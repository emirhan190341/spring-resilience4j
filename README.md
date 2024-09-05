# spring-resilience4j


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
