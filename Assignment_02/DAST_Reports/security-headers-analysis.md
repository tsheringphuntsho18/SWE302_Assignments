## Overview

To enhance the security posture of the RealWorld Conduit application, several HTTP security headers were implemented on both the backend (Go) and frontend (deployment configuration). These headers help mitigate common web vulnerabilities such as clickjacking, MIME sniffing, XSS, and insecure transport.

## Implemented Security Headers

### Backend (Go)

The following middleware was added to `hello.go`:

```go
router.Use(func(c *gin.Context) {
    c.Header("X-Frame-Options", "DENY")
    c.Header("X-Content-Type-Options", "nosniff")
    c.Header("X-XSS-Protection", "1; mode=block")
    c.Header("Strict-Transport-Security", "max-age=31536000; includeSubDomains")
    c.Header("Content-Security-Policy", "default-src 'self'")
    c.Next()
})
```

### Frontend

Security headers were configured in the build/deployment environment (e.g., using Nginx, Apache, or a cloud provider’s custom headers configuration).

#### Explanation of Each Header

- **X-Frame-Options: DENY**  
  Prevents the site from being embedded in an iframe, protecting against clickjacking attacks.

- **X-Content-Type-Options: nosniff**  
  Stops browsers from MIME-sniffing a response away from the declared content-type, reducing exposure to drive-by downloads and user-uploaded content attacks.

- **X-XSS-Protection: 1; mode=block**  
  Enables the browser’s XSS filter and instructs it to block the page if an attack is detected.  
  _Note: Modern browsers may ignore this header, but it is still a defense-in-depth measure._

- **Strict-Transport-Security: max-age=31536000; includeSubDomains**  
  Enforces HTTPS by telling browsers to only communicate with the server over secure connections for one year, including all subdomains.

- **Content-Security-Policy: default-src 'self'**  
  Restricts the sources from which content (scripts, styles, images, etc.) can be loaded to only the same origin, mitigating XSS and data injection attacks.

#### Verification

After implementation, a ZAP scan confirmed the presence of all configured security headers in HTTP responses.

#### Summary

Implementing these headers significantly reduces the risk of several common web vulnerabilities. Regularly review and update security headers as best practices evolve.
