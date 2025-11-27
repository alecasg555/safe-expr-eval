# Security Policy

## Supported Versions

We release patches for security vulnerabilities for the following versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |

## Reporting a Vulnerability

We take the security of `safe-expr-eval` seriously. If you discover a security vulnerability, please follow these steps:

### How to Report

1. **DO NOT** open a public issue
2. Report security issues through GitHub Security Advisories: https://github.com/alecasg555/safe-expr-eval/security/advisories/new
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

### What to Expect

- **Initial Response**: Within 48 hours
- **Status Update**: Within 7 days
- **Fix Timeline**: Depends on severity
  - Critical: Within 7 days
  - High: Within 14 days
  - Medium: Within 30 days
  - Low: Next release cycle

### Disclosure Policy

- We will coordinate disclosure with you
- Security advisories will be published after a fix is available
- Credit will be given to reporters (unless anonymity is requested)

## Security Best Practices

When using `safe-expr-eval`:

1. **Validate Input**: Always validate expressions from untrusted sources
2. **Limit Variables**: Only expose necessary variables to expressions
3. **Sanitize Functions**: Be careful when adding custom functions
4. **Error Handling**: Implement proper error handling around evaluation
5. **Rate Limiting**: Consider rate limiting for user-provided expressions

### Example: Safe Usage

```typescript
import { Parser } from 'safe-expr-eval';

function evaluateUserExpression(expr: string, data: object) {
  // 1. Validate expression length
  if (expr.length > 1000) {
    throw new Error('Expression too long');
  }

  // 2. Create parser with limited scope
  const parser = new Parser();
  
  // 3. Only expose safe functions
  parser.functions.abs = Math.abs;
  parser.functions.min = Math.min;
  parser.functions.max = Math.max;

  // 4. Wrap in try-catch
  try {
    return parser.evaluate(expr, data);
  } catch (error) {
    console.error('Evaluation error:', error);
    return null;
  }
}
```

## Known Security Considerations

### What We Protect Against

✅ **Code Injection**: No `eval()` or `Function()` constructor used
✅ **Prototype Pollution**: Proper object handling
✅ **Denial of Service**: Limited recursion depth
✅ **Type Confusion**: Strong type checking

### What You Should Protect Against

⚠️ **Untrusted Functions**: Be careful when adding custom functions
⚠️ **Resource Exhaustion**: Implement timeouts for complex expressions
⚠️ **Sensitive Data**: Don't expose sensitive variables to untrusted expressions

## Security Updates

Subscribe to security updates by:
- Watching this repository
- Following our [releases](https://github.com/alecasg555/safe-expr-eval/releases)
- Checking [npm advisories](https://www.npmjs.com/advisories)

## Acknowledgments

We appreciate the security research community's efforts in making our software more secure. Responsible disclosure is valued and acknowledged.

---

Last updated: November 2025
