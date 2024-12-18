# How to Review PRs Like a 10x Developer

## 1. First Pass: Big Picture
- What problem does this PR solve?
- Is the solution appropriate for the problem?
- Are there architectural concerns?
- Does it follow team conventions?

## 2. Code Quality Checklist
- Code readability and maintainability
- Proper error handling
- Performance considerations
- Security implications
- Test coverage
- Documentation updates

## 3. Specific Areas to Check

```typescript
// 1. Variable/Function Naming
❌ Bad
function x(a, b) { return a + b }

✅ Good
function calculateTotal(price: number, tax: number) { 
  return price + tax 
}

// 2. Error Handling
❌ Bad
try {
  await fetchData()
} catch (e) {
  console.log(e)
}

✅ Good
try {
  await fetchData()
} catch (error) {
  logger.error('Failed to fetch data:', { error, context: 'dataFetch' })
  throw new CustomError('DataFetchError', error)
}

// 3. Side Effects
❌ Bad
function processUser(user) {
  user.lastLogin = Date.now()  // Mutates input
  return user
}

✅ Good
function processUser(user) {
  return {
    ...user,
    lastLogin: Date.now()
  }
}
```

## 4. Security Review
- SQL injection vulnerabilities
- XSS vulnerabilities
- Authentication/Authorization checks
- Sensitive data exposure
- Input validation

## 5. Testing Review
```typescript
// Check for:
- Unit tests
- Integration tests
- Edge cases
- Error scenarios
- Performance tests (if needed)
```

## 6. Performance Considerations
- Database query optimization
- Unnecessary re-renders
- Memory leaks
- Large bundle sizes
- API call efficiency

## 7. Constructive Feedback
❌ Bad:
"This code is messy"

✅ Good:
"Consider extracting this logic into a separate function to improve readability:
```typescript
function validateUserInput(input: UserInput): ValidationResult {
  // validation logic here
}
```

## 8. PR Review Template
```markdown
### Overview
- [ ] Code follows team style guide
- [ ] Documentation is updated
- [ ] Tests are included
- [ ] Performance impact considered

### Security
- [ ] Input validation
- [ ] Authentication/Authorization
- [ ] Data protection

### Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Edge cases covered

### Comments
- Strengths:
  - 
- Suggestions:
  - 
```

## 9. Best Practices
1. Review in multiple passes
2. Use automated tools first
3. Test the changes locally
4. Be timely with reviews
5. Be constructive and specific
6. Ask questions instead of making assumptions

## 10. Tools to Use
- Linters (ESLint, etc.)
- Type checkers (TypeScript)
- Code coverage tools
- Security scanners
- Performance profilers

## 11. Response Time Guidelines
- Small PR (< 200 lines): 1 day
- Medium PR (200-1000 lines): 2 days
- Large PR (> 1000 lines): Request breaking into smaller PRs

## 12. Final Checklist
✅ Code works as intended
✅ Tests pass and cover edge cases
✅ Documentation is updated
✅ No security vulnerabilities
✅ Performance is acceptable
✅ Code is maintainable
✅ Follows team standards

## Remember:
- Focus on important issues first
- Be constructive and respectful
- Consider the context and constraints
- Share knowledge and explain your reasoning
- Use automated tools to handle basic checks
- Review the actual changes, not just the diff
- Consider the long-term maintainability