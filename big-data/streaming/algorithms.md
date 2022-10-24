# Algorithms

##  Random Sampling with a Reservoir

Random sampling is a common technique in data streaming.

Use case: *YouTube*

The goal is to perform a real-time statistical analysis of the watched videos. On the surface it seems pretty easy, but, how do we know that data is random?

**Reservoir sampling** is based on the notion of reservoir.
We cannot hold a predetermined number of stream values but, when a new value arrives, we can probabilistically determine whether to add it to out collection or to discard it.

The reservoir is always filled with the first *r* values in the stream, where r is the size of the reservoir.

For any element, the probability to go inside or outside the reservoir is the same.

![](reservoir.jpg)

## Hyperloglog 

Count distinct elements.

Use case: *Facebook*

The goal is to count the users that are connected to the website.

There are two general categories for the *count-distinct* problem.
**Hash functions** can be used to translate input items to a uniform distribution in some bounded domains.

**Order statistics-based** algorithms:

- Based on the evaluation of the order statistics
- Since the distribution is uniform, we know that the lowest value is 1/number of elements
- ONly the minimum value must be stored (no need to store hash tables)

**Bit-pattern-based** (HyperLogLog) algorithms:

The basis of the HyperLogLog algorithm is the following observation:

The cardinality of a multi-set of uniformly distributed random numbers can be estimated calculating the maximum number of leading zeros in the binary representation of each number in the set.

Given a binary string, the probability to observe:

- 1 initial zero: 50%
- 2 initial zeros: 25%
- 3 initial zeros: 12.5%
- n initial zeros: 1/n

if I know the maximum number of initial zeros ever observed is n, than i can guess that it must have taken approximately 2^n attempts.

![](hyperloglog.jpg)

