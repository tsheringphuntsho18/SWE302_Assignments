## Vulnerability Summary

- **Total Vulnerabilities Found:** 7
- **OWASP Top 10 Mapping:**
  - A1: Injection (SQL Injection, XSS)
  - A3: Sensitive Data Exposure
  - A5: Broken Access Control
  - A6: Security Misconfiguration
- **Risk Distribution:**
  - **Critical:** 1
  - **High:** 2
  - **Medium:** 3
  - **Low:** 1

## Critical/High Severity Vulnerabilities

### 1. SQL Injection
- **Risk:** Critical
- **URLs Affected:**  
  - `POST http://localhost:8080/api/articles`
  - `GET http://localhost:8080/api/articles?author=`
- **CWE:** CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')
- **OWASP Category:** A1:2017-Injection
- **Description:**  
  User input is not properly sanitized, allowing attackers to inject SQL commands.
- **Attack Details:**  
  ZAP was able to manipulate the `author` parameter to bypass authentication and retrieve all articles.
- **Evidence:**  
  Request: `GET /api/articles?author=' OR 1=1--`  
  Response: All articles returned, regardless of author.
- **Impact:**  
  Attackers can access, modify, or delete data in the database.
- **Remediation:**  
  Use parameterized queries or ORM methods to handle user input.

### 2. Cross-Site Scripting (XSS)
- **Risk:** High
- **URLs Affected:**  
  - `POST http://localhost:4100/api/articles`
  - `GET http://localhost:4100/article/<slug>`
- **CWE:** CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')
- **OWASP Category:** A7:2017-Cross-Site Scripting (XSS)
- **Description:**  
  User-supplied content is rendered without proper escaping, allowing script injection.
- **Attack Details:**  
  ZAP injected `<script>alert(1)</script>` in article content, which executed in the browser.
- **Evidence:**  
  Article page rendered the injected script.
- **Impact:**  
  Attackers can execute arbitrary JavaScript in users' browsers, steal cookies, or perform actions on behalf of users.
- **Remediation:**  
  Sanitize and escape all user input before rendering.

### 3. Sensitive Data Exposure (Session Cookie Without Secure Flag)
- **Risk:** High
- **URLs Affected:**  
  - `http://localhost:4100/`
- **CWE:** CWE-614: Sensitive Cookie in Non-HTTPS Session
- **OWASP Category:** A3:2017-Sensitive Data Exposure
- **Description:**  
  Session cookies are set without the `Secure` flag, making them vulnerable to interception.
- **Attack Details:**  
  ZAP detected cookies transmitted over HTTP.
- **Evidence:**  
  Set-Cookie header lacks `Secure` attribute.
- **Impact:**  
  Attackers on the same network can intercept session cookies.
- **Remediation:**  
  Set the `Secure` and `HttpOnly` flags on all cookies.

## Expected Findings

- **SQL Injection:** Confirmed (see above)
- **Cross-Site Scripting (XSS):** Confirmed (see above)
- **Security Misconfiguration:** Missing security headers, directory listing enabled
- **Sensitive Data Exposure:** Session cookie issues, server version headers exposed
- **Broken Authentication:** No account lockout on repeated failed logins
- **Insecure Direct Object References:** Not detected in this scan
- **Missing Function Level Access Control:** Not detected in this scan
- **Cross-Site Request Forgery (CSRF):** No CSRF tokens detected on forms
- **Using Components with Known Vulnerabilities:** None detected by ZAP
- **Unvalidated Redirects:** Not detected in this scan

## API Security Issues

- **Lack of Rate Limiting:**  
  No rate limiting detected on login or article creation endpoints.
- **Verbose Error Messages:**  
  API returns stack traces on invalid requests.
- **Information Disclosure:**  
  Server version and error details exposed in responses.
- **Authorization Bypass:**  
  No evidence found in this scan.
- **Mass Assignment:**  
  Not detected, but review recommended.

## Frontend Security Issues

- **XSS in Article Content:**  
  Confirmed (see above)
- **XSS in Comments:**  
  Not detected, but review recommended.
- **DOM-based XSS:**  
  Not detected in this scan.
- **Insecure localStorage Usage:**  
  No sensitive data found in localStorage.

## Exported Reports

- **HTML Report:** `zap-active-report.html`
- **XML Report:** `zap-active-report.xml`
- **JSON Report:** `zap-active-report.json`

**Summary:**  
The ZAP active scan identified several critical and high risk vulnerabilities, including SQL Injection, XSS, and insecure cookie handling. Immediate remediation is required to address these issues and improve the application's security posture.