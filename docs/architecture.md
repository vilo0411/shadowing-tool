# Architecture Document

**Dự án:** Shadowing Tool
**Stack:** React + Vite
**Cập nhật:** 2026-01-28

---

## 1. Tech Stack

```yaml
Frontend:
  - Framework: React 18
  - Build Tool: Vite 5
  - Language: TypeScript
  - Styling: Tailwind CSS
  - State Management: Zustand
  - Icons: Lucide React

Storage:
  - Primary: localStorage
  - Backup: IndexedDB (cho data lớn nếu cần)

Development:
  - Linting: ESLint
  - Formatting: Prettier
  - Package Manager: pnpm (hoặc npm)

Deployment:
  - Static hosting: Vercel / Netlify / GitHub Pages
  - Or: Local (npm run dev)
```

---

## 2. System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                        Browser                               │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐   │
│  │   File API   │    │  HTML5 Media │    │ localStorage │   │
│  │  (Input)     │    │    API       │    │  (Storage)   │   │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘   │
│         │                   │                   │            │
│         ▼                   ▼                   ▼            │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                    React App                         │    │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌────────┐  │    │
│  │  │  Zustand │  │ SRT     │  │ Media   │  │Progress│  │    │
│  │  │  Store   │  │ Parser  │  │ Player  │  │ Store  │  │    │
│  │  └─────────┘  └─────────┘  └─────────┘  └────────┘  │    │
│  │                                                      │    │
│  │  ┌─────────────────────────────────────────────┐    │    │
│  │  │              UI Components                   │    │    │
│  │  │  LoadView | PlayerView | ChunkList | Editor │    │    │
│  │  └─────────────────────────────────────────────┘    │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**Data Flow:**
```
User selects files
       │
       ▼
┌──────────────┐     ┌──────────────┐
│ Media File   │────▶│ createObjectURL
│ (.mp4/.mp3)  │     │ for playback │
└──────────────┘     └──────────────┘
       │
       ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Subtitle File│────▶│ SRT Parser   │────▶│ Chunks Array │
│ (.srt)       │     │              │     │ in Zustand   │
└──────────────┘     └──────────────┘     └──────────────┘
                                                 │
                                                 ▼
                                          ┌──────────────┐
                                          │ localStorage │
                                          │ (progress)   │
                                          └──────────────┘
```

---

## 3. Cấu trúc thư mục

```
src/
├── main.tsx                 # Entry point
├── App.tsx                  # Root component + routing
├── index.css                # Global styles + Tailwind
│
├── components/
│   ├── ui/                  # Base UI components
│   │   ├── Button.tsx
│   │   ├── Modal.tsx
│   │   ├── Input.tsx
│   │   └── Slider.tsx
│   │
│   ├── layout/              # Layout components
│   │   ├── Header.tsx
│   │   └── Sidebar.tsx
│   │
│   └── features/            # Feature-specific components
│       ├── FileLoader/
│       │   ├── FileLoader.tsx
│       │   └── DropZone.tsx
│       │
│       ├── Player/
│       │   ├── MediaPlayer.tsx
│       │   ├── PlayerControls.tsx
│       │   ├── SpeedControl.tsx
│       │   └── LoopToggle.tsx
│       │
│       ├── ChunkList/
│       │   ├── ChunkList.tsx
│       │   ├── ChunkItem.tsx
│       │   └── ChunkFilter.tsx
│       │
│       ├── ChunkEditor/
│       │   ├── ChunkEditor.tsx
│       │   ├── TimingInput.tsx
│       │   └── MergeSplitControls.tsx
│       │
│       └── Subtitle/
│           └── SubtitleDisplay.tsx
│
├── hooks/
│   ├── useMediaPlayer.ts    # Media playback logic
│   ├── useKeyboardShortcuts.ts
│   ├── useChunkNavigation.ts
│   └── useLocalStorage.ts
│
├── stores/
│   ├── useAppStore.ts       # Main app state (Zustand)
│   └── useProgressStore.ts  # Progress persistence
│
├── lib/
│   ├── srtParser.ts         # SRT file parser
│   ├── timeUtils.ts         # Time formatting utilities
│   └── storage.ts           # localStorage wrapper
│
├── types/
│   └── index.ts             # TypeScript types/interfaces
│
└── constants/
    └── index.ts             # App constants (shortcuts, speeds, etc.)
```

---

## 4. Data Model

### Core Types

```typescript
// types/index.ts

// Chunk từ SRT file
interface Chunk {
  id: string;              // unique id (generated)
  index: number;           // thứ tự trong list
  startTime: number;       // milliseconds
  endTime: number;         // milliseconds
  text: string;            // subtitle text
  originalIndex: number;   // index gốc từ SRT (để track sau edit)
}

// Session state - lưu trong Zustand
interface Session {
  mediaFile: File | null;
  mediaUrl: string | null;  // object URL for playback
  subtitleFile: File | null;
  chunks: Chunk[];
  editedChunks: Chunk[];    // chunks sau khi user edit (merge/split)
  currentChunkIndex: number;
  isPlaying: boolean;
  isLooping: boolean;
  playbackSpeed: number;    // 0.5 - 1.5
}

// Progress - lưu trong localStorage
interface FileProgress {
  fileId: string;           // hash of filename + size
  fileName: string;
  lastChunkIndex: number;
  completedChunks: number[]; // indexes of done chunks
  chunkEdits: ChunkEdit[];   // edits user made
  lastAccessedAt: number;    // timestamp
}

// Chunk edit history (để có thể restore)
interface ChunkEdit {
  type: 'timing' | 'merge' | 'split';
  originalChunks: number[];  // indexes affected
  newChunks: Chunk[];        // resulting chunks
  timestamp: number;
}

// Player state
interface PlayerState {
  currentTime: number;
  duration: number;
  isPlaying: boolean;
  playbackRate: number;
}
```

### Storage Schema

```typescript
// localStorage keys
const STORAGE_KEYS = {
  PROGRESS: 'shadowing_progress',     // Record<fileId, FileProgress>
  SETTINGS: 'shadowing_settings',     // UserSettings
  RECENT_FILES: 'shadowing_recent',   // string[] (file names)
};

// Settings
interface UserSettings {
  defaultSpeed: number;
  autoLoop: boolean;
  theme: 'light' | 'dark' | 'system';
  shortcuts: Record<string, string>;  // customizable shortcuts
}
```

---

## 5. State Management (Zustand)

### Main Store

```typescript
// stores/useAppStore.ts

interface AppState {
  // Session
  session: Session;

  // Actions - File loading
  loadMediaFile: (file: File) => void;
  loadSubtitleFile: (file: File) => void;
  clearSession: () => void;

  // Actions - Playback
  play: () => void;
  pause: () => void;
  toggleLoop: () => void;
  setSpeed: (speed: number) => void;

  // Actions - Navigation
  goToChunk: (index: number) => void;
  nextChunk: () => void;
  prevChunk: () => void;

  // Actions - Chunk editing
  updateChunkTiming: (chunkId: string, start: number, end: number) => void;
  mergeChunks: (startIndex: number, endIndex: number) => void;
  splitChunk: (chunkId: string, splitTime: number) => void;

  // Actions - Progress
  markChunkDone: (index: number) => void;
  markChunkUndone: (index: number) => void;
}
```

### Progress Store (with persistence)

```typescript
// stores/useProgressStore.ts

interface ProgressState {
  progresses: Record<string, FileProgress>;

  // Actions
  saveProgress: (fileId: string, progress: FileProgress) => void;
  loadProgress: (fileId: string) => FileProgress | null;
  clearProgress: (fileId: string) => void;
  getRecentFiles: () => FileProgress[];
}
```

---

## 6. Component Hierarchy

```
App
├── LoadView (when no files loaded)
│   └── FileLoader
│       ├── DropZone (media)
│       └── DropZone (subtitle)
│
└── PracticeView (when files loaded)
    ├── Header
    │   ├── FileName
    │   ├── ProgressBar
    │   └── SettingsButton
    │
    ├── MainContent
    │   ├── MediaPlayer
    │   │   └── <video> or <audio> element
    │   │
    │   ├── SubtitleDisplay
    │   │   └── Current chunk text
    │   │
    │   └── PlayerControls
    │       ├── PrevButton
    │       ├── PlayPauseButton
    │       ├── NextButton
    │       ├── LoopToggle
    │       ├── SpeedControl
    │       └── MarkDoneButton
    │
    └── Sidebar
        ├── ChunkFilter (all/done/not done)
        └── ChunkList
            └── ChunkItem (for each chunk)
                ├── Checkbox (done status)
                ├── Index
                ├── Text preview
                └── EditButton → opens ChunkEditor modal

Modal: ChunkEditor
├── TimingInput (start)
├── TimingInput (end)
├── Preview button
├── MergeButton (if multiple selected)
├── SplitButton (with time picker)
└── Save/Cancel
```

---

## 7. Key Hooks

### useMediaPlayer

```typescript
// hooks/useMediaPlayer.ts

interface UseMediaPlayerReturn {
  mediaRef: RefObject<HTMLVideoElement | HTMLAudioElement>;
  currentTime: number;
  duration: number;
  isPlaying: boolean;

  play: () => void;
  pause: () => void;
  seek: (time: number) => void;
  setPlaybackRate: (rate: number) => void;
}

// Handles:
// - Playing chunk from start to end time
// - Auto-stop at chunk end
// - Loop logic (replay when chunk ends)
// - Speed control
```

### useKeyboardShortcuts

```typescript
// hooks/useKeyboardShortcuts.ts

// Handles global keyboard events:
// Space → play/pause
// ArrowRight/J → next chunk
// ArrowLeft/K → prev chunk
// L → toggle loop
// [ → speed down
// ] → speed up
// Enter → mark done + next
// ? → show shortcuts modal
```

---

## 8. SRT Parser

```typescript
// lib/srtParser.ts

/**
 * Parse SRT content to chunks
 *
 * SRT Format:
 * 1
 * 00:00:01,000 --> 00:00:04,000
 * Hello world
 *
 * 2
 * 00:00:05,000 --> 00:00:08,000
 * How are you?
 */

function parseSRT(content: string): Chunk[] {
  // 1. Split by double newline (entries)
  // 2. For each entry:
  //    - Line 1: index (ignore, generate our own)
  //    - Line 2: timestamp (parse start --> end)
  //    - Line 3+: text (join with space)
  // 3. Convert timestamp to milliseconds
  // 4. Generate unique IDs
  // 5. Return Chunk[]
}

function parseTimestamp(ts: string): number {
  // "00:01:23,456" → 83456 (milliseconds)
}

function formatTimestamp(ms: number): string {
  // 83456 → "00:01:23,456"
}
```

---

## 9. Quyết định kiến trúc (ADRs)

### ADR-001: Client-side only architecture

- **Context:** App cần load local files và lưu progress
- **Decision:** Không dùng backend, mọi thứ xử lý trong browser
- **Rationale:**
  - Local files không cần upload
  - Progress lưu localStorage đủ dùng
  - Đơn giản hóa deployment (static files)
- **Consequences:**
  - Không sync được giữa devices
  - File paths không được nhớ (browser security)

### ADR-002: Zustand cho state management

- **Context:** Cần quản lý app state (session, chunks, playback)
- **Decision:** Dùng Zustand thay vì Redux/Context
- **Rationale:**
  - Lightweight (~1KB)
  - Không boilerplate
  - Built-in persistence middleware
  - TypeScript support tốt
- **Consequences:** Đủ cho app này, dễ migrate nếu cần

### ADR-003: Object URL cho media playback

- **Context:** Cần play local files trong browser
- **Decision:** Dùng `URL.createObjectURL(file)` để tạo playable URL
- **Rationale:**
  - Browser native, không cần library
  - Works với video và audio
  - Không cần upload file
- **Consequences:**
  - URL chỉ valid trong session
  - Cần revoke để tránh memory leak

### ADR-004: Edited chunks stored separately

- **Context:** User có thể edit timing, merge, split chunks
- **Decision:** Giữ original chunks, store edits separately
- **Rationale:**
  - Có thể reset về original
  - Không mất data gốc
  - Dễ implement undo (future)
- **Consequences:** Cần logic để merge original + edits khi render

---

## 10. Performance Considerations

### Media Playback
- Sử dụng `timeupdate` event throttled (mỗi 100ms) để update UI
- `seeking` và `seeked` events để handle chunk navigation
- Preload metadata only: `<video preload="metadata">`

### Chunk List
- Virtualized list nếu > 500 chunks (dùng react-window)
- Memoize ChunkItem components
- Debounce search/filter input

### Storage
- Batch writes to localStorage (không save mỗi action)
- Cleanup old progresses (> 100 files → xóa oldest)

---

## 11. File Structure Summary

```
shadowing-tool/
├── docs/
│   ├── brief.md
│   ├── prd.md
│   └── architecture.md
│
├── src/
│   ├── components/
│   ├── hooks/
│   ├── stores/
│   ├── lib/
│   ├── types/
│   └── constants/
│
├── public/
│   └── favicon.ico
│
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
├── tailwind.config.js
└── README.md
```
