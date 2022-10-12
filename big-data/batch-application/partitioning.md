# Partitioning

Data in RDD are split into multiple partitions, which serve two purposes:

1. parallelize computation across workers and CPU cores
2. Minimize network traffic for data exchange between executors

If not specified, SPark sets the number of partitions automatically. The number of partitions are important as one task is run for each partition:

Too few partitions results in less concurrency and risks from data skewness, while too many partitions results in excessive overhead in managing small tasks.

**Rule of thumb:**

- Lower bound: 2 partitions for each core
- Upper bounds:
    - each task should take at least 100/200 ms to execute
    - a block worth of data

When in doubt, more partitions is usually better.

## RDD Partitioning Criteria

The partitioning criteria is used to:

- Put values that belong to the same key in the same partition
- Define how the key should be distributed in different partitions
- No control over the specific worker node a partition goes to

Partition criteria triggers shuffle operations so, forcing a partitioning criteria on a RDD is costly and there is no explicit control over which worker node each key goes on.

**Different partitioning data:**

1. **Hash Partitioning:** hashing using the Java hashCode
2. **Range Partitioning:** distributes data into uniform ranges
3. **Custom Partitioning:** user-defined partitioning

**When is it useful?**

If I repartition an RDD based on some criteria, then I know that all the values with the same key will end up in the same partition.

## Shuffling

Shuffling is the mechanism used to re-distribute data across partitions. It is necessary to compute some operations but it is costly and complex.

![](hash.jpg)

![](sort.jpg)

![](tungsten.jpg)

In time, Spark has provided a number of shuffling implementations:

- **Hash shuffle:** each map task creates a file for every reducer. [In this article is explained clearly (kinda)](https://medium.com/@philipp.brunenberg/understanding-apache-spark-hash-shuffle-b9aed2d587b0)
    - Each executor holds a pool of files
    - A single group contains a file for every reducer
    - An executor contains as many groups as the mapper than can run in parallel in the executor itself
- **Sort shuffle:**
- **Tungsten sort:**