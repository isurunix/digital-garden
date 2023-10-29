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

- Decide where to place the limiter
    - Client side rate limiter
