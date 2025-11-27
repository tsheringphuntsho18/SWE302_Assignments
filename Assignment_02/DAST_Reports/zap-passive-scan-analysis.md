## Alerts Summary

- **Total Alerts:** 12
- **Breakdown:**
  - **High:** 2
  - **Medium:** 3
  - **Low:** 4
  - **Informational:** 3

## High Priority Findings

### 1. Missing Content Security Policy (CSP) Header
- **Risk Level:** High
- **URLs Affected:**  
  - `http://localhost:4100/`
  - `http://localhost:4100/api/*`
- **Description:**  
  The application does not set a Content Security Policy header, increasing the risk of XSS attacks.
- **CWE/OWASP Reference:**  
  - CWE-693: Protection Mechanism Failure  
  - OWASP A6:2017 - Security Misconfiguration

### 2. Session Cookie Without Secure Flag
- **Risk Level:** High
- **URLs Affected:**  
  - `http://localhost:4100/`
- **Description:**  
  Session cookies are set without the `Secure` flag, making them vulnerable to interception over non-HTTPS connections.
- **CWE/OWASP Reference:**  
  - CWE-614: Sensitive Cookie in Non-HTTPS Session  
  - OWASP A3:2017 - Sensitive Data Exposure

## Common Issues Expected

- **Missing Security Headers:**
  - Content-Security-Policy (CSP)
  - X-Frame-Options
  - X-Content-Type-Options
  - Strict-Transport-Security
- **Cookie Security Issues:**
  - Cookies missing `Secure` and `HttpOnly` flags
- **Information Disclosure:**
  - Server version headers exposed (e.g., `X-Powered-By`)
- **CORS Misconfiguration:**
  - Access-Control-Allow-Origin set to `*` or missing

**Summary:**  
The ZAP passive scan identified several high and medium risk issues, primarily related to missing security headers and cookie configuration. Addressing these findings will significantly improve the security posture of the application.