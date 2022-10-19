# Architecture

![](architecture.jpg)

There is a lot of data movements among the different phases, which can be handles directly in the application that carry out the different activities or relying on a **message queueing service**.

This message queueing service works as a message bus connected to the single applications.

## Message Queuing Service

The message queueing tier handles the transportation of data between different tiers.

- By decoupling the pipeline of operations, each node in the cluster will do one job only
- Message queueing provides a solid framework for a safe communication between such nodes
- Message queuing handles funneling of n data streams to m consumers

In the message queueing system, we have he notion of a **borker**, which handles the communication, by means of queues.
The broker creates different queues, one for each topic, and keeps the data for a certain amount of time.

![](broker.jpg)

We can decide the level of **delivery semantics**, which refers to the level of precision in sending the message form producer to consumer.

- **Exactly once**: a message is never lost and is read once and only once 
- **At most once**: a message may get lost, but it will never be read twice
- **At least once**: a message will never be lost, but it may be read twice
    - Less control but you avoid data getting lost (tradeoff)




