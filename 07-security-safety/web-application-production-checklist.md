# Web Application Production Security Checklist

## Introduction

Transitioning a web application from development to production requires careful security checks to protect against various threats. This comprehensive checklist covers essential security practices to implement before deploying your application, with specific focus on applications developed using agent-based coding tools like Cursor IDE.

## Pre-Deployment Security Checklist

The following 17-point checklist is adapted from comprehensive security best practices and specifically enhanced for projects developed with AI assistance:

### 1. Authentication and Authorization

| Check | Description | Implementation Guidelines |
|-------|-------------|---------------------------|
| **Implement Strong Authentication** | Ensure MFA, strong password policies, secure password storage | Use established auth libraries and frameworks; validate against OWASP standards |
| **Review Authorization Logic** | Implement RBAC, least privilege principle, secure session management | Audit access control logic to identify potential bypass routes |
| **Update Auth Callback URLs** | Ensure callbacks point to production domains | Systematically check all callback configurations |
| **Disable Debug Modes** | Turn off debug modes in production (e.g., NextAuth debug) | Scan for debug flags and development-only settings |

### 2. Input and Output Handling

| Check | Description | Implementation Guidelines |
|-------|-------------|---------------------------|
| **Sanitize All User Inputs** | Use DOMPurify and context-specific sanitization | Review all input handling logic; test with malicious inputs |
| **Implement Server-Side Validation** | Use validation libraries like Zod for robust input checking | Create comprehensive validation schemas |
| **Protect Against XSS** | Validate/sanitize inputs, implement CSP | Add Content Security Policy in next.config.js; audit template rendering |
| **Prevent SSRF Attacks** | Whitelist allowed hostnames and validate URLs | Analyze all URL handling and API communication |

### 3. Data Protection

| Check | Description | Implementation Guidelines |
|-------|-------------|---------------------------|
| **Ensure Data Encryption** | Use SSL/TLS, encrypt sensitive data at rest | Verify encryption implementation for all sensitive data |
| **Manage Environment Variables** | Do not commit .env files, use deployment configs | Scan for hardcoded secrets or exposed variables |
| **Update Production Variables** | Set production-specific variables | Verify environment configuration through CI/CD checks |
| **Configure Production Databases** | Use PostgreSQL/MySQL, apply connection pooling | Generate secure database configuration templates |

### 4. API and Network Security

| Check | Description | Implementation Guidelines |
|-------|-------------|---------------------------|
| **Implement API Abstraction** | Prevent direct database calls from client-side | Audit for secure API architecture patterns |
| **Apply Rate Limiting** | Limit API calls to prevent abuse | Implement robust rate-limiting logic (see Advanced Rate Limiting section) |
| **Configure WAF Protection** | Deploy Web Application Firewall | Analyze potential attack vectors to configure WAF rules |

### 5. Development and Deployment

| Check | Description | Implementation Guidelines |
|-------|-------------|---------------------------|
| **Audit Dependencies** | Run `npm audit`, update packages regularly | Automate dependency health checks in CI pipeline |
| **Fix All Linter Errors** | Address code quality issues before deployment | Configure CI to fail on linting errors |

## Error Handling Best Practices for Production

Proper error handling is critical for both security and user experience:

### Implementation Guidelines

1. **Display Generic Messages**
   - Use user-friendly error messages without revealing system details
   - Never expose database structure, stack traces, or internal error codes
   - Example: Use "Unable to process request" instead of detailed SQL errors

2. **Implement Environment-Specific Error Handling**
   - Create different error handling modes for development vs. production
   - In development: detailed errors with stack traces and context
   - In production: sanitized responses with appropriate HTTP status codes

3. **Centralize Error Handling**
   - Create a central error handler to ensure consistent messaging
   - Log detailed information server-side while displaying minimal info to users
   - Categorize errors to provide appropriate user guidance without technical details

4. **Maintain HTTP Standards**
   - Return appropriate HTTP status codes even with sanitized messages
   - Include standard error response structure (e.g., `{error: {message: "", code: ""}}`)
   - Consider implementing error references for support inquiries

5. **Separate Error Logging**
   - Implement separate error logging systems with different retention policies
   - Consider using structured logging to facilitate error analysis
   - Ensure error logs don't contain sensitive personal information

## Production Debug Code Removal

Debugging code can inadvertently expose sensitive information in production:

### Implementation Guidelines

1. **Remove Console Statements**
   - Systematically remove all `console.log` statements before deployment
   - Console logs can expose sensitive data to anyone using browser dev tools
   - Example risk: `console.log("User authentication failed for:", userEmail, password);`

2. **Implement Environment-Aware Logging**
   - Create conditional logging based on environment variables
   ```javascript
   // Example of environment-aware logging
   const logger = {
     debug: (message, data) => {
       if (process.env.NODE_ENV !== 'production') {
         console.log(`DEBUG: ${message}`, data);
       }
     },
     error: (message, error) => {
       // Always log errors but sanitize in production
       console.error(`ERROR: ${message}`, 
         process.env.NODE_ENV === 'production' 
           ? {message: error.message} 
           : error
       );
     }
   };
   ```

3. **Automate Removal During Build**
   - Configure build tools like Webpack with plugins to strip console statements
   - Example webpack configuration:
   ```javascript
   // webpack.config.js
   const TerserPlugin = require('terser-webpack-plugin');
   
   module.exports = {
     // ... other config
     optimization: {
       minimizer: [
         new TerserPlugin({
           terserOptions: {
             compress: {
               drop_console: process.env.NODE_ENV === 'production',
             },
           },
         }),
       ],
     },
   };
   ```

4. **Configure Linting Rules**
   - Set up ESLint with no-console rule to prevent accidental inclusion
   ```json
   // .eslintrc.json
   {
     "rules": {
       "no-console": ["error", { "allow": ["warn", "error"] }]
     }
   }
   ```

5. **Use Production Logging Services**
   - For necessary production logging, use proper logging services with access controls
   - Consider services like Sentry, LogRocket, or application-specific logging infrastructure

## Advanced API Rate Limiting

Comprehensive rate limiting is essential for API security in production:

### Implementation Guidelines

1. **Implement Granular Limits**
   - Set different thresholds for various endpoints based on their sensitivity
   - Create different limits for authenticated vs. unauthenticated users
   - Example configuration:
   ```javascript
   // Rate limiting configuration example
   const rateLimits = {
     // Public endpoints
     '/api/public/*': {
       windowMs: 15 * 60 * 1000, // 15 minutes
       max: 100 // limit each IP to 100 requests per windowMs
     },
     // Authentication endpoints (more strict to prevent brute force)
     '/api/auth/*': {
       windowMs: 15 * 60 * 1000,
       max: 10
     },
     // Authenticated user endpoints (per user)
     '/api/user/*': {
       windowMs: 60 * 60 * 1000, // 1 hour
       max: 1000,
       keyGenerator: (req) => req.user.id // based on user ID, not IP
     }
   };
   ```

2. **Implement Adaptive Rate Limiting**
   - Adjust limits based on traffic patterns and user behavior
   - Increase limits for trusted users with good history
   - Implement progressive penalties for repeated violations

3. **Include Proper Headers**
   - Add informative headers to API responses:
     - `X-RateLimit-Limit`: Total requests allowed in period
     - `X-RateLimit-Remaining`: Requests remaining in period
     - `X-RateLimit-Reset`: Time when limit resets
     - `Retry-After`: Seconds to wait before retrying (when limited)

4. **Return Appropriate Status Codes**
   - Use HTTP 429 'Too Many Requests' when limits are exceeded
   - Include clear guidance on when to retry
   - Example response:
   ```json
   {
     "error": "Rate limit exceeded",
     "message": "You have exceeded the request rate limit. Please wait and try again later.",
     "retryAfter": 120
   }
   ```

5. **Distributed Rate Limiting**
   - For multi-server deployments, use Redis or similar in-memory data stores
   - Ensure rate limits are synchronized across services
   - Consider using specialized rate limiting services for complex implementations

## OWASP Top 10 Vulnerabilities (2025)

When deploying applications to production, pay special attention to these top security vulnerabilities:

| Rank | Vulnerability | Prevention Strategy |
|------|--------------|---------------------|
| 1 | SQL Injection | Implement parameterized queries and ORM tools; validate all database interactions |
| 2 | Broken Access Control | Create comprehensive access control tests; implement principle of least privilege |
| 3 | Broken Authentication | Use established authentication libraries; implement MFA and proper session management |
| 4 | Cross-Site Scripting (XSS) | Implement Content Security Policy and input sanitization; use frameworks with built-in XSS protection |
| 5 | Cross-Site Request Forgery | Implement synchronizer token patterns and SameSite cookies; generate and validate CSRF tokens |
| 6 | Server-Side Request Forgery | Build URL validation and whitelist systems; restrict network access from application servers |
| 7 | Security Misconfiguration | Generate secure default configurations; use infrastructure as code with security checks |
| 8 | Cryptographic Failures | Implement current cryptographic standards; avoid custom encryption implementations |
| 9 | Weak User Passwords | Create robust password validation and security policies; implement credential compromise checking |
| 10 | Missing Function-Level Access Control | Generate comprehensive authorization tests; implement consistent access check patterns |

## Security Monitoring and Incident Response

Once deployed to production, continuous security monitoring is essential:

1. **Regular Security Scanning**
   - Schedule automated vulnerability scans
   - Perform periodic penetration testing
   - Review security logs for suspicious patterns

2. **Security Update Process**
   - Establish a clear process for applying security patches
   - Create emergency procedures for critical vulnerabilities
   - Document security update testing requirements

3. **Incident Response Plan**
   - Develop a detailed incident response plan
   - Define roles and responsibilities during security incidents
   - Create communication templates for different types of incidents

## Statistics and Industry Benchmarks

Current industry statistics highlight the importance of web application security:

- SQL injection accounts for 23% of critical vulnerabilities worldwide (Statista, 2024)
- Global data breach costs average $4.88 million per incident (IBM Security Report, 2024)
- According to CWE-209, improper error handling remains a common weakness leading to information leakage
- Kong Inc. research shows implementing different rate limits for authenticated vs. unauthenticated users provides better security balance
- Companies with comprehensive security testing programs detect vulnerabilities 24 days faster on average (Veracode State of Software Security Report, 2024)

## Resources and References

- [OWASP Top 10 Web Application Security Risks](https://owasp.org/Top10/)
- [Indusface Blog: A Comprehensive Web Application Security Checklist](https://www.indusface.com/blog/a-comprehensive-web-application-security-checklist/)
- [Iterasec: Common Web Application Vulnerabilities in 2025](https://iterasec.com/blog/common-web-application-vulnerabilities/)
- [Web App Security: 2025 Complete Guide by Savvycom Software](https://savvycomsoftware.com/blog/web-app-security-complete-guide-2025/)
- [10 Best Web Scanners for Website Security In 2025](https://cybersecuritynews.com/web-scanners/)
- [Complete Web Application Security Testing Checklist](https://www.spaceotechnologies.com/blog/web-application-security-testing-checklist/)
- [Security Checklist for Web Application by SANS Institute](https://www.sans.org/cloud-security/securing-web-application-technologies/)
