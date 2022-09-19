# Big Data Infrastructures

**Scaling** -> big data does not fit into a single drive (or a single machine). 
Big data requires a lot of computer resources.

## SMP Architecture

Symmetric Multi Processing, which is adopted by traditional RDBSM has physical limits regarding the number of devices that can be mounted, as well as a BUS bottleneck.

## Scaling

- Scale-up (adding more resources like processors, RAM, disk or upgrading the machine)
- Scale-out (adding more machines)

## MPP Architecture

Massively Parallel Processing:
- Several processors, equipped with their own RAM and disks, collaborating to solve a single problem by splitting it in several interdependent tasks.
- This architecture requires specialized hardware. 
- Vendor lock-in may be an issue with this architecture.

## Cluster Architecture (scale-out)

A cluster is a group of linked computers (nodes), working together closely so that in many respects they form a single computer.

- There is no vendor lock-in
- Every node is a system on its own, capable of independent operations 
- Unlimited scalability 

Compute nodes are stored on racks
- There can be many racks of computer nodes
- The nodes on a single rack are connected by a network
- Racks are connected by another level of network

## Scale-up vs Scale-out

Scaling-up PROS:
- Lower power consumption and utility costs
- Less challenging to implement
- Lower licensing costs
- Specialized hardware and software

Scaling-out PROS:
- Infinite scaling
- Generalist hardware and software
- Cheaper machines
- Usually cheaper overall
- Commodity Hardware
    - Hardware that can be seen as a commodity
    - Large range of vendors

## Multiple Clusters

Having a single large cluster allows you to avoid data silos, leading to a simpler governance.

However, multiple clusters are inevitable within medium-large enterprise settings:
- Resiliency (every cluster sits within a single point of failure)
- Software development (mitigate the risk of impacting critical production environments by isolating configuration, integration, or evolution testing and deployment)
- Workload isolation (hardware resources tuned for specific workloads)
- Legal separation
- Independent storage and compute

With the success of cloud services, the independent storage and compute solution for big data clusters is on the rise
- DATA LOCALITY (locate the resource that deal with specific data near to that data, avoiding to move data from one machine to another)

Machines that store data are usually up and running 24/7 as data must be persistent. 

## Other distributed architectures

**Grid Computing**
- Similar to cluster computing
- Each node is set to perform a different task

**High Performance Computing**
Massively parallel systems specifically developed to solve CPU-intensive tasks.
Big data systems are mostly data-intensive.

![](hpc.jpg)




