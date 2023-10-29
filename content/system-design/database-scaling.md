---
title: Database Scaling
tags:
  - database
  - scaling
date: 2023-09-16
---

When a system grows it's data also grows with it requiring the database to be scaled in order to handle loads of data.
The two broad approches for scaling a database is vertical scaling and horizontal scaling.
Same as in scaling an application server vertical database scaling refers to allocating more resources to the database
server and horizonal scaling referes to techiniques like database replication and database sharding

However as in every system design it all depends on the context. Before blindly jumping into replication or sharding there might be other possible optimization you could do to scale your database to support the load

## Query Optimizations & Connection Pools

Effectively these things are should be there from the begining if you are planning to cater to a large amount of requets with low latency. But it never hurts to pay the first attention to these basics and make sure things are in order. 

- Proper indexing
- Add redundant columns (denormalize data) to reduce join queries
- Use connection pooling and monitor/tweak connection pool capacity

## Vertical Scaling

Vertical scaling refers to adding more resources to the database server to improve it's performance and support the load.
This can be either CPU/RAM or Disk depending on the requirement.

### Pros

- Easier to do since there is zero configuration for the database. Simply increase the CPU/RAM/Disk for the server instance
- Powerful instances are already available via major cloud providers (Ex: Amazon RDS with 24TB of RAM)

**Note**
> Stackoverflow supported 10 million MAU with a single master database

### Cons

- Single point of failure
- Limited by the possible maxed-out configuration for the server
- Cost

## Database Replication

Database replication can be handy when you want to improve read performance for database queries. In most of the cases `read` operations are more frequent than `write` operations in the database. Replication allows us to distribute `read` operations between multiple instances thus reducing the load on the `source` node and improving `read` throughput.

To setup replication

- Configure two or more database servers having the same schema
- Configure the DBMS to use one of the nodes as the `source` and others as `replica` nodes.

`replica` nodes will receive copies of data from the `source` node and will only support `read` operations. All `write` operations should be directed to the `source` node.

### Pros
- Improved performance as now we can perform multiple read operations in parallel from each `replica` node
- Improved reliability as multiple copies of data are available in case of a failure in one node
- High Availability can be achieved by having replicas in multiple locations

### Cons
- Single `source` configuration will not improve write performance significantly
- If the `source` server fails promoting a `replica` node as the new `source` could require some manual work

## Horizontal Scaling


---
**References:**
- [A Guide To Understanding Database Scaling Patterns - FreeCodeCamp](https://www.freecodecamp.org/news/understanding-database-scaling-patterns/)
- [How to set up replication in MySQL - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-replication-in-mysql)
- System Design Interview – An insider's guide, Second Edition - Alex Xu



