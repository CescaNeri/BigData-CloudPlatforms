# NoSQL DBMS

Relational DBMS have lots of features like ACID properties, data integration and normalization schemas, standard model and query language and robustness.

However, a part from advantages, RDBMS have also weaknesses:

- Impedance mismatch (data are stored according to the relational model, but applications to modify them typically rely on the object-oriented model)
- Painful scaling-out (not suited for a cluster architecture and distributed environments)
- Consistency vs latency (today's applications require high reading/writing throughput with low latency)
- Schema rigidity (schema evolution is often expensive)

## NoSQL in the Big Data world

NoSQL systems are mainly used for operational workloads (**OLTP**).

Big data technologies are mainly used for analytical workloads (**OLAP**).

## Data Models

One of the key challenges is to understand which one fits best with the required application:

![](data-model.jpg)


**Graph Data Model**

Each database contains one or more graphs. 
Each graph contains **vertices** and **arcs**.

- Vertices: usually represent real-world entities
- Arcs: represent direct relationships between the vertices


The graph data model is intrinsically different form the others:

- It is focused on the relationships rather than on the entities per-se
- It has limited **scalability** (it is often possible to shard a graph on several machines without cutting several arcs)
- It is a data-driven modeling
- It is based on the concept of **encapsulation**

**Document Data Model**

Each database contains one or more collections, each of which contains a list of documents (JSON).
Each document contains a set of fields and each field correspond to a key-value pair.

Depending on the **query** that I want to carry out, I can choose the most suitable model.

**Key-value Data Model**

Each database contains one or more collections and each collection contains a list of key-value pairs.

**Wide Column Data Model**

Each database contains one or more column families and each column family contains a list of row in the form of a key-value pair.

Each column is a key-value pair itself while rows specify only the columns for which a value exists.

The query language expressiveness is in between key-value and document data models.

## Sharding Data

One of the strengths of NoSQL systems is their **scale-out capability**.
Two aspects must be considered when deploying on a cluster:

- Sharding (subdividing data in shards that are stored in different machines)
- Replication  (data is copied on several nodes)

**Master-Slave Replication**

Master: manager of the data

- It handles each and every write operation
- It can be chosen or drawn

Slaves: enables read operations

- It is in sync with the master
- It can become master if the latter fails

Pros and cons of the master-slave replication:

PROS:

- Easy handles many read requests
- Useful when the workload mainly consists of reads
- Useful to avoid write conflicts

CONS:

- The master is a bottleneck
- Delay in write propagation can be a source of inconsistency
- Not ideal when the workload mainly consists or writes

**Peer-to-peer Replication**

Each node has the same importance and can handle write operations.
The loss of a node does not compromise reads nor writes.

Pros and cons of the peer-to-peer replication:

PROS:

- The failure of a node does not interrupt read or write requests
- Write performances easily scale by adding new nodes

CONS:

- Conflicts
- Delay in write propagation can be a source of inconsistency
- Two users may update the same value from different replicas