# Managing Consistency

RDBMS come from decades of widespread usage with a strong focus on data consistency and years of research activities to optimize performances.

NoSQL systems are designed to succeed  where RDBMS fail:

- Strong focus on data sharding and high availability
- Quite simple systems
- Speed and manageability rather than consistency at all costs

## CAP Theorem

According to the CAP theorem, only two of the following three properties can be guaranteed:

- **Consistency** (every node returns the same, most recent, successful write)
- **Availability** 
- **Partition Tolerance** (the system continues to function and upholds its consistency guarantees in spite of network partitions)

In distributed systems, network partitioning is inevitably a possibility.

It sacrifices consistency over latency.

## PACELC Theorem

It is an evolution of the CAP theorem.

```java
if {Partition} then {Availability or Consistency?}
Else 
    {Latency or Consistency?}
```

![](consistency.jpg)

Inconsistencies are tolerated in this area because latency is considered as being much more important.

For example, for Amazon, it is more important that users can navigate quickly rather than consistency in products data.

This because inconsistency does not impact user experience that much as latency would be.