---
title: Scaling for Millions of Users
tags:
  - system-design
  - scaling
date: 2023-09-15
---

**Scenario** : A system that caters large number of users with a web front-end and a mobile app.

Things to consider

- Choice of Database
    - For most cases relational database like MySQL would work
    - Things to consider when going for NoSQL
        - Application requires super law latency
        - Unstructured data or data has no relations
        - Need to store a massive amount of data
          
- Scale the application tier
    - Decide whether horizontal or vertical scaling
    - Vertical scaling is limited by CPU, Memory, Space and cost
    - Horizontal scaling require adding new components like load balancers and changing the application to be able to share load
      
- Scale the database ([[database-scaling]])
    - Database Replication
    - Database Sharding
 
- Use Caching and CDN for static assets
    - Avoid frequent calls to database
    - Improve performance
      
- Make the application/web tier stateless
    - Mitigates issue with stateless web tier/sticky sessions
    - Easier horizontal scaling

- Support multiple data centers
    - Geo Routing
    - Geo DNS
    - Disaster Recovery
    - Availability

- Decouple the components and make processes async, Introduce message queues
    - RabbitMQ
    - Kafka

---
**References:**
- System Design Interview – An insider's guide, Second Edition - Alex Xu
