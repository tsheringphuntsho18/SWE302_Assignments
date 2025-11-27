# k6 Spike Test Analysis

## 1. Spike Impact
- **System Response to Sudden Load Increase:**  
  The system failed to handle the sudden spike in virtual users (from 10 to 100 VUs). All requests during the test failed.

- **Error Rate During Spike:**  
  - **Error rate:** 100% (120 out of 120 requests failed)
  - **Successful checks:** 0%
  - No requests returned a 200 status code.

- **Response Time During Spike:**  
  - **Average response time:** 60 seconds
  - **Median response time:** 60 seconds
  - **Max response time:** 60 seconds
  - All requests appear to have timed out at the 60-second mark, indicating the backend was unresponsive or unreachable during the spike.

## 2. Recovery
- **How Long to Recover After Spike?**  
  - The system did not recover during the test window. All requests, including those after the spike, continued to fail.
  - No successful responses were observed during the recovery period.

- **Any Cascading Failures?**  
  - Yes. The failure persisted beyond the spike period, suggesting a cascading or persistent backend failure.

- **System Stability After Spike:**  
  - The system remained unstable after the spike, with 100% failure rate throughout the test.

## 3. Real-World Scenarios
- **Marketing Campaign Launch:**  
  - If a campaign drove a sudden surge in users, the system would be unable to serve any requests, resulting in a poor user experience and lost opportunities.

- **Viral Content:**  
  - A sudden influx of users due to viral content would overwhelm the system, causing total service outage.

- **Bot Attack Mitigation:**  
  - The system is highly vulnerable to denial-of-service from sudden spikes, as it cannot recover or serve requests under such conditions.

## 4. Findings and Recommendations

### Findings
- The backend could not handle a sudden increase in load, resulting in 100% failed requests and maximum timeouts.
- The system did not recover within the test duration, indicating a need for better resilience and resource management.

### Recommendations
- **Implement auto-scaling** for backend services to handle sudden spikes.
- **Optimize backend performance** and ensure sufficient resources (CPU, memory, DB connections) are available.
- **Introduce rate limiting** and queueing mechanisms to prevent total service failure during spikes.
- **Monitor and alert** on high error rates and timeouts to enable rapid response.
- **Test and tune** server and database configuration for high concurrency scenarios.


## 5. Supporting Evidence
- k6 terminal output
![k6](./assets/k6_load.png)

## Conclusion 
The system is currently unable to handle sudden spikes in traffic, resulting in total service outage and prolonged unavailability. Immediate improvements in scalability, resilience, and resource management are required to support real-world spike scenarios.