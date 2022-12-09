# Big Data Architectures

There are a lot of problems related to distributed architectures, especially concerning parallelization:

- Communication between workers
- Access to shared resources
- Parallelization and concurrency

The solution is to have single computer -> **Data Center**

![](datacenter.jpg)

The core is the **framework provider**, which is the set of software modules that handles the abstraction of the complexity of the computer system and makes it visible as if it was a single entity.

It provides general resources or services to be used by the Big Data Application Provider in the creation of the specific application.

The **data provider** introduces new data or information feeds into the Big Data system. It can be anything from a sensor to a human and performs the following activities:

- Collecting and persisting the data
- Providing transformation functions
- Creating the metadata describing the data source
- Enforcing access rights on data access and establishing contracts for data access authorizations
- Making the data accessible through suitable programmable push or pull interfaces and mechanisms
- Publishing the availability of the information and the means to access it

**System Orchestrator** -> manages application (both a human being or a program)

- Integrates the required application activities into ana operational vertical system
- Configure and manage the other components of the Big Data architecture to implement one ore more workloads
- Monitor workloads and system to verify the meeting of quality requirements
- Elastically assign and provision additional physical or virtual resources

![](arch.jpg)

A Big Data architecture is composed of:

1. **Data sources**: data stores, static files, real-time sources
2. **Data storage**: distributed file store or database
3. **Batch processing**: Long-running batch jobs to filter, aggregate, and prepare the data for analysis
4. **Analytical data store**: serve the processed data in a structured format that can be queried using analytical tool
5. **Analysis and reporting**: Traditional OLAP and BI tools, interactive exploration, analytical notebooks

## Analytical Applications

- **Batch Analysis:** Take a large amount of data and run analysis
    - Run on demand
    - Takes a lot of time
- **Stream Analysis** We devised an algorithm that runs continuously 
    - Real-time results
    - Useful for monitoring

Can we run both batch and stream on the same set of data?

**Lambda architecture**
Most trivial way to handle this problem. It consists in duplicating the data in order to apply both analysis.
Data goes through two path:

- Hot path (timely, real-time, less accurate data)
- Cold path (less timely but more accurate data)

**Kappa architecture**
We can simplify the problem and handle everything a stream problem.
Stream and batch application are different BUT we can run batch analysis on a stream engine.
Data flows through a single patch, using a stream processing system. 

**Lambda vs Kappa**
Lambda is easier but it needs parallel development and maintenance of two parallel pipelines. 
Kappa is the ongoing trend. A streaming engine can handle a bounded dataset and a well-designed streaming systems provide a strict superset of batch functionality.





