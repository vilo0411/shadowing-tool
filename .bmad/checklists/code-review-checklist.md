# ✅ Code Review Checklist

> Checklist cho @reviewer khi review code

## Functionality

- [ ] Code implement đúng requirements trong story
- [ ] Acceptance criteria được đáp ứng
- [ ] Edge cases được handle
- [ ] Error cases có proper handling

## Code Quality

### TypeScript
- [ ] Không có `any` type (trừ khi justified)
- [ ] Interfaces/Types được define đúng
- [ ] Không có `@ts-ignore` hoặc `@ts-expect-error`
- [ ] Strict mode compliant

### Clean Code
- [ ] Naming rõ ràng, descriptive
- [ ] Functions ngắn, single responsibility
- [ ] Không có code duplication
- [ ] Comments giải thích "why", không phải "what"
- [ ] Không có console.log (dùng proper logger)
- [ ] Không có TODO/FIXME bị bỏ quên

### React Specific
- [ ] Components có proper prop types
- [ ] useEffect có cleanup function (nếu cần)
- [ ] Dependencies array đầy đủ
- [ ] Không có infinite re-render risks
- [ ] Keys unique trong lists
- [ ] Không có memory leaks

## Error Handling

- [ ] Try-catch cho async operations
- [ ] Error messages user-friendly
- [ ] Errors được log đúng cách
- [ ] Graceful degradation

## Security

- [ ] Input validation
- [ ] Auth checks ở protected routes
- [ ] Không expose sensitive data
- [ ] SQL injection prevention (ORM)
- [ ] XSS prevention

## Performance

- [ ] Không có unnecessary re-renders
- [ ] Expensive calculations được memoize
- [ ] Images optimized
- [ ] No N+1 queries
- [ ] Proper loading states

## Maintainability

- [ ] Follow existing code patterns
- [ ] File ở đúng folder
- [ ] Consistent với codebase style
- [ ] Dễ đọc và hiểu
- [ ] Có thể test được

## Documentation

- [ ] Complex logic có comments
- [ ] API endpoints documented
- [ ] README updated (nếu cần)
- [ ] explain/ docs created (nếu feature mới)

## Testing

- [ ] Happy path tested
- [ ] Error cases tested
- [ ] Edge cases tested
- [ ] No broken tests

## Final

- [ ] Build không có errors
- [ ] Lint không có errors/warnings
- [ ] Chạy được locally
- [ ] Ready cho production
