# Assignment 2: Static & Dynamic Application Security Testing (SAST & DAST)

## Executive Summary
This report summarizes the results of comprehensive security testing performed on the application using both Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST) tools. The assessment leveraged industry-standard tools including SonarQube and Snyk for SAST, and OWASP ZAP for DAST. The objective was to identify security vulnerabilities, evaluate the effectiveness of existing security controls, and recommend remediation steps to enhance the application's security posture.

[Frontend github repo](https://github.com/tsheringphuntsho18/react-redux-realworld-example-app)   

[Backend github repo](https://github.com/tsheringphuntsho18/golang-gin-realworld-example-app)

## Key Findings Across All Tools

### Static Application Security Testing (SAST)
- **SonarQube** identified several code quality issues and security hotspots in both backend and frontend codebases. Most issues were related to code maintainability, input validation, and potential injection points.
- **Snyk** detected a number of vulnerable dependencies in both backend and frontend projects. Some high-severity vulnerabilities were found, particularly in outdated third-party libraries. Snyk also provided automated remediation suggestions, some of which were applied and verified.

### Dynamic Application Security Testing (DAST)
- **OWASP ZAP** uncovered several security issues during both passive and active scans. Key findings included missing or misconfigured security headers, potential cross-site scripting (XSS) vectors, and information disclosure through HTTP responses.
- The API security analysis highlighted insufficient input validation and lack of proper authentication mechanisms on certain endpoints.

### General Observations
- Most critical vulnerabilities were related to outdated dependencies and improper input validation.
- Security headers such as `Content-Security-Policy`, `X-Frame-Options`, and `Strict-Transport-Security` were either missing or not properly configured.
- Some issues were fixed as part of this assignment, as documented in the remediation and fixes reports.

## Remaining Risks
- **Unresolved Vulnerabilities:** A few medium and low-severity vulnerabilities remain, primarily due to dependencies that do not yet have secure versions or require significant code refactoring.
- **Security Hotspots:** Some code areas flagged by SonarQube as security hotspots require manual review and further mitigation.
- **Incomplete Security Headers:** Not all recommended security headers have been implemented, leaving the application partially exposed to certain web-based attacks.
- **Authentication and Authorization Gaps:** Some API endpoints lack robust authentication and authorization checks, increasing the risk of unauthorized access.
- **Ongoing Dependency Management:** Continuous monitoring and timely updates of third-party libraries are necessary to prevent future vulnerabilities.

## Conclusion:
While significant progress has been made in identifying and mitigating security risks, ongoing vigilance and periodic security assessments are essential to maintain a strong security posture. The remaining risks should be prioritized and addressed in a timely manner, with particular attention to updating dependencies, reinforcing security headers and ensuring comprehensive authentication and authorization mechanisms are in place.
