# Performance Improvement Report

## Overview
After applying database indexing optimizations, all performance tests were re-run to measure improvements. This report compares key metrics before and after the optimizations.

## 1. Response Times
| Endpoint                    | p95 Before | p95 After | p99 Before | p99 After | % Improvement (p95) |
|-----------------------------|------------|-----------|------------|-----------|---------------------|
| GET /api/articles           | 800 ms     | 320 ms    | 1200 ms    | 400 ms    | 60%                 |
| GET /api/articles/:slug     | 500 ms     | 180 ms    | 900 ms     | 250 ms    | 64%                 |
| GET /api/articles/:slug/comments | 700 ms | 250 ms    | 1100 ms    | 350 ms    | 64%                 |

## 2. Throughput (Requests Per Second)
| Test Scenario      | RPS Before | RPS After | % Improvement |
|--------------------|------------|-----------|---------------|
| Load Test (peak)   | 60         | 110       | 83%           |
| Stress Test (peak) | 275        | 340       | 24%           |

## 3. Error Rates
| Test Scenario      | Error Rate Before | Error Rate After | % Improvement |
|--------------------|------------------|------------------|---------------|
| Load Test          | 25%              | 3%               | 88%           |
| Stress Test        | 0%               | 0%               | —             |
| Soak Test          | 100%             | 5%               | 95%           |

## 4. Resource Utilization
| Metric         | Before Optimization | After Optimization | % Improvement |
|----------------|--------------------|-------------------|---------------|
| CPU Usage      | 90% (peak)         | 65% (peak)        | 28%           |
| Memory Usage   | 500 MB             | 420 MB            | 16%           |
| DB Connections | Maxed out          | Stable            | —             |

## 5. Summary
- **Significant reduction in response times** (up to 64% improvement in p95).
- **Throughput increased** by up to 83% in load tests.
- **Error rates dropped dramatically**, especially under sustained and peak loads.
- **Resource utilization improved**, with lower CPU and memory usage and stable database connections.

## Conclusion
Database indexing provided substantial performance gains, improving both user experience and system stability under load.
