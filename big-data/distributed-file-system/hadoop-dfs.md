# Hadoop Distributed File System

The first thing that software has to provide is **abstraction**, as we want to interact with the disks of the machines as if it was a single machine.
We want a single reference and we want to talk to a single entity.
- Master-Slave architecture 
A single entity works as a master and handles the storage of the data with a set of slaves that are running of single machines.


The software needs to deal with **big data**:
- Files may be bigger than single disks
- We need to split files into smaller blocks and store them on different machines

ALso, **fault tolerance** is of key importance: disks can fail, machines can be unreachable, but data should always be available.
- we can store multiple copies of each block




