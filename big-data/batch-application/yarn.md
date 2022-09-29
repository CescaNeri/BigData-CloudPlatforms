# YARN - Yet ANother Resource Negotiator

In the same cluster, I want to run some programs and applications. The problem regards how these computations allocate resources.

The resource negotiator:

- In charge of assigning units of work
- Has a global view of the resources  available in the cluster
- Decides where and when each uint of work should be allocated and with how many resources
- Uses a scheduling policy to manage concurrency
- Avoids over-instantiation of processes 
- Handles fault-tolerance

Potentially, we can run as many process as we want on each machine but we do not want to overload it.

YARN provides APIs for requesting and working with cluster resources.

- It is a general framework (works with any kind of application you want to run)
- Application are written using analytical frameworks

## Main Daemons
YARN work with the master/slave mechanism:

- Resource Manager (ultimate authority that arbitrates among all the applications)
- Node Manager (per-node slave)
    - In charge of running containers which run applications (virtual abstract entities associated with a certain amount of resources. We have a virtual environment that run applications)

For each application. there is one container that runs a special process that in charge of coordinating the single operation.

**Coordination** happens on two levels:

1. Resource Manager, composed by two components:
    - Application Manager (start the application - accept request from client and start the machine)
    - Scheduling component (decides where resources should be allocated)
2. For each application, we have another process (**application master process**) that manages the resources of each application

Application execution consists of the following steps:

1. A client program submits the application, including the necessary specifications to launch the application-specific AMP itself
2. The RM assumes the responsibility to negotiate a specified container in which to start the AMP and then launches it
3. The AMP registers with the RM
4. The AMP negotiates appropriate resources containers
5. On successful container allocations, the AMP launches the container by providing the container launch specification
6. The application code executing within the container provides necessary information
7. During the application execution, the client that submitted the program communicates directly with the AMP to get status and updates
8. Once the application is complete, the AMP de-registers with the RM and shuts down, allowing its own container to be repurposed

## YARN Scheduler

YARN provides a choice of schedulers and configurable policies:

- FIFO scheduler (useless)
- Fair Scheduler (with multiple applications that want to access the resource, the scheduler will balance the resources among the two applications)
    - Problem related to prediction of execution time as resources are split
- Capacity Scheduler (the amount of resources is divided in two profiles - fixed amount)
    - Each application run within a profile have access to a fixed amount of resources
    - Execution time is predictable but there may be a waste of resources

## Data Locality

When the scheduler needs to identify the resources to allocate, it does so following the data locality principle.
The point is to exploit cluster typology and data block replication to apply the data locality principle. 

*When computation involves large set of data, it is cheaper to move code to data rather than data to code*






