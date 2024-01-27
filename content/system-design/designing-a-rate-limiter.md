---
title: Designing a Rate Limiter
tags:
  - system-design
date: 2023-09-22
draft: true
---

# Designing a Rate Limiter

## Requirements

- Limit excessive requests
- Low latency
- Low memory foot print
- Should support distributed rate limiting
- Exception handling. Should show meaningful error message to user when being throttled
- High fault tolerance. Failure in rate-limiter should not affect the rest of the system

## High Level Design

### Placement of Functionality (Where to put the limiter)
- **Client side rate limiter**
  While it is technically possible to place the rate limiter on client side this can be highly unpredictable as it can be easily forged. Also we may not always have the control of the client. So it doesn't make much sense to place a rate-limiter in client app ^6ba237
- **Server side rate limiter**
  Rate limiter can be placed on the app server it self as a part of the application service
    ```mermaid
          graph LR
          A[Client] -- HTTP/HTTPS --> api-service[api-service]
          subgraph api-service
          app-service; 
          app-service <-.-> rate-limitter
          end
    ```
    - **Pros**
        - Cannot be forged easily like the client-side implementation
        - Can be deployed together with the application service
    - **Cons**
        - Tightly coupled to app service making it not reusable
        - Added complexity in the app service which does not exactly address any functional/business requirement
        - Tight coupling requires app service to be redeployed even for a change in the rate-limiter.
- **Rate Limiter Service as a middle-ware**
  Another option would be develop the rate-limiter as a separate service and place it as middle-ware layer between the client and the application service. Most of the time we see this approach in use where API gateway implements the rate limiting functionality as well.
  
  ```mermaid
  graph LR
  A[Client] -- HTTP/HTTPS --> B[Rate Limiter] --> app-service
  ```
  - **Pros**
      - Cannot be forged easily
      - Loosely coupled with the app service
      - Reusable
      - Can be deployed separately
  - **Cons**
      - One more component to maintain

**Summary**

> Client side rate limiter is never a good choice. [[#^6ba237]]
> 
> Most often a middle-ware rate limiter makes sense since most time we already have a api-gateway in place and it would be wise to have the rate limiter over there. However this depends on the company's tech stack and the current application eco-system.

### Rate Limiting Algorithms

Once we figured out where to place our rate limiter next thing we need to decide is which algorithm we are going to use to limit the number of requests. There are couple of popular algorithms used in for rate limiting.

1. [Token Bucket](token-bucket)
2. Leaking Bucket
3. Fixed Window Counter
4. Sliding Window
5. Sliding Window Counter

## High Level Architecture

![[rate-limiter-high-level.excalidraw.png]]
