# Assignment 3: Performance Testing & End-to-End Testing

[Frontend github repo](https://github.com/tsheringphuntsho18/react-redux-realworld-example-app)

[Backend github repo](https://github.com/tsheringphuntsho18/golang-gin-realworld-example-app)

## Summary

### Performance Baseline Established

- Load, stress, spike, and soak tests were conducted using k6.
- Baseline metrics: ~70 RPS, avg response time 0.7 ms, p95 1.35 ms under moderate load.
- Error rate exceeded threshold at peak concurrency (25% failed requests).

### Bottlenecks Identified

- High CPU usage and database connection saturation during peak load.
- Certain endpoints (`POST /api/articles`, authentication) failed consistently under load.
- Backend instability and timeouts observed at higher concurrency.

### Optimizations Implemented

- Increased database connection pool size.
- Added caching for frequently accessed endpoints.
- Improved error handling and rate limiting.
- Backend code profiling and targeted optimizations for slow endpoints.

### End-to-End (E2E) Test Coverage

- E2E tests automated for core user flows: registration, login, article CRUD, favoriting, and tag filtering.
- Tests executed using Cypress; results captured and analyzed.
- [E2E test screenshot](./assets/e2e_test.png)

### Browser Compatibility Findings

- Cross-browser tests performed on Chrome, Firefox, and Edge.
- No major UI or functional issues found; minor CSS inconsistencies noted and fixed.
- [Cross-browser test report](./cross-browser-testing-report.md)

### Key Learnings

- System performs well under moderate load but requires backend and DB tuning for higher concurrency.
- Automated E2E and browser tests are essential for regression prevention and user experience assurance.
- Performance testing helps uncover hidden bottlenecks and optimize system robustness.
