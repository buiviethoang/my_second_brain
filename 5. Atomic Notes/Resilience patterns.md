2025-09-16 21:55
Status: 
Topic: 
Tags: [[system design]]
## Main

**Resilience patterns** are design strategies used in software architecture, especially in distributed systems like microservices, to ensure that applications remain available, reliable, and stable despite failures, disruptions, or high demand.


Key resilience patterns include:

- **Retry Pattern:** Automatically retries a failed operation due to temporary issues like network glitches or brief service unavailability, often with exponential backoff to avoid overwhelming the system.
    
- **Fallback Pattern:** Provides an alternative response or method when a service is unavailable, enabling graceful degradation of functionality instead of complete failure.
    
- **Timeout Pattern:** Sets limits on how long a system waits for responses before considering the operation failed, preventing long waits that can cascade failures.
    
- **Circuit Breaker Pattern:** Monitors for failures and stops requests to a failing service temporarily to prevent overload, allowing it time to recover.

Other important patterns include **Bulkhead** (isolating resources to prevent failure spread), **Cache** (store responses to reduce load), **Rate Limitin**g (control request rates), Redundancy (duplicate components for failover), and **Load Shedding** (dropping low priority requests under heavy load).

Benefits of using resilience patterns include improved availability, minimized impact of failures, faster recovery, better user experience with fewer disruptions, and enhanced scalability.

Examples of companies effectively using these patterns include Netflix (circuit breaker with Hystrix), Amazon (bulkhead isolation), Uber (timeouts and retries), and Spotify (fallback mechanisms).

## References