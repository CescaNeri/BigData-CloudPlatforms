# Processing Big Data

When you are on a distributed architecture, it is important to manage the distribution of machines.
Many problems can happen in distributed environments. 

Since data is spread across machines, it is important to replicate those data. 
Also, it will not be possible to update data at the same time so you will need to deal with consistency (eventual consistency).
- it may happen that data collected at the same time may refer to different momentos.

## Big Data Software Stack

New programming environments designed to get their parallelism not from a supercomputer but from computer clusters.

**Apache Hadoop**

- automate the management of low level applications
- low-level tool, more advanced tools can be applied to it

It is a software library (framework) that allows for the distributed processing of large data sets across clusters of computers using simple programming models.

Rather than relying on hardware to deliver high-availability and reliability, the library itself is designed to detect and handle failures at the application layer, so as to deliver a highly-available service on top of a cluster of computers.

**Hadoop Modules**

- HDFS (Hadoop Distributed File System) - storage
    - layer that handles the storage of data across different machines
    - provides ABSTRACTION on the storage of data
- YARN (Yet Another Resource Negotiator) - computation
    - decides which unit of application runs in which machine
    - if some unit of work fails in some machine, it will recreate it in another machine
- Map Reduce - analysis
    - YARN-based system for parallel processing of large data sets

**On top of Hadoop**

Many different programming solutions can be applied on hadoop:
1. Analytics (batch)
    - simple/complex computations over large amounts of stored data
2. Interactive (real-time)
    - operational perspective 
3. Streaming (near-real-time)
    - continuous analytics
    - analysis run on continuously incoming data 
    - there is no much time and resources, you need to adopt some approximation algorithms 


