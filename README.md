# spring-resilience4j

The **Resilience4j** library provides **Circuit Breaker**, **Retry**, and **Rate Limiter** features to enhance system resilience against failures. The **Circuit Breaker** prevents system instability by halting requests when certain error thresholds are exceeded. **Retry** reattempts operations a set number of times when errors occur, while the **Rate Limiter** ensures requests are processed within defined rate limits, preventing system overload.

```yaml
server:
  port: 8080

management:
  health:
    circuitbreakers:
      enabled: true
  endpoints:
    web:
      exposure:
        include: health
  endpoint:
    health:
      show-details: always

resilience4j:
  circuitbreaker:
    instances:
      serviceA:
        registerHealthIndicator: true
        eventConsumerBufferSize: 10
        failureRateThreshold: 50
        minimumNumberOfCalls: 5
        automaticTransitionFromOpenToHalfOpenEnabled: true
        waitDurationInOpenState: 5s
        permittedNumberOfCallsInHalfOpenState: 3
        slidingWindowSize: 10
        slidingWindowType: COUNT_BASED

  retry:
    instances:
      serviceA:
        max-attempts: 5
        waitDuration: 10s

  ratelimiter:
    instances:
      serviceA:
        registerHealthIndicator: false
        limitForPeriod: 10
        limitRefreshPeriod: 10s
        timeoutDuration: 3s

```
