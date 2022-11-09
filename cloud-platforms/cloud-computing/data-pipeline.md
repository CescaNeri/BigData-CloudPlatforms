# Building Data Pipelines in the Cloud

**Data pipeline:** a sequence of operations to transform and consume raw data

![](pipeline.jpg)

The pyramid abstracts tons of techniques which if we want to provide them as services, architecting data pipelines on cloud requires:

- Standardization
- Integration
- Orchestration
- Accessibility through simple APIs

**Data pipeline in AWS:**

![](aws.jpg)

With stream data, data are *pushed* in the data platform, while with batch data, data are *pulled* from the repository.

**Data pipeline in Google cloud:**

![](google.jpg)

The organization of the services is the same, both in AWS and in Google.

## Pipeline Organization

1. Ingestion  (collect raw data from transaction, logs and IoT devices)
2. Transformation (make data consumable by sorting, aggregating, and applying business logic to produce meaningful analytical datasets)
3. Consume data (querying and BI tools)

![](organization.jpg)

This is not a sharp taxonomy, for example data streams can also be processed during the ingestion phase and databases can serve both processing and serving capabilities.

## Storage

The goal of storage is to persist data.
To choose the most suitable storage platform, we need to consider:

- Storage model (how data are organized)
- Access frequency (how often do we access data)
- Analysis to be performed

**AWS S3** - serverless AWS storage service

AWS S3 saves data as objects within buckets. An object is composed of a file and any metadata that describes that file.

**Buckets** are logical containers for objects.

Benefits of AWS S3:

- Centralized data architecture
- Decoupling of storage from compute and data processing

**Access frequency (AWS)**

Object storage classes:

- Standard (general purpose)
- Infrequent (rapid access)
- One Zone-IA (lower cost option for infrequently accessed data)
- Glacier (low cost storage class for data archiving)
- Deep Glacier (long-term retention for data accessed once or twice a year)
- Intelligent-Tiering (move objects between access tiers when access patterns change)

**Lifecycle** configuration: a set of rules that define actions that Amazon S3 applies to a group of objects.

We can identify two types of actions:

1. Transition (object transition to another storage class)
2. Expiration (AWS deletes expired objects)

## Organizing Data Lake

Having consistent principles on how to organize your data is important to build standardized pipelines with the same design with regard to where read/write.
Also, standardization makes it easier to manage your pipelines at scale and helps users search for data in the storage.

![](data-lake1.jpg)

![](data-lake2.jpg)

Using folders to organize data inside areas into a logical structure can be useful:

> Namespace

Logically group multiple pipelines together.

> Pipeline name

Each data pipeline should have a name that reflects its purpose.

> Data source name

Ingestion layer will assign a name to each data source you bring into the platform

> BatchId

Unique identifier for any batch of data that is saved into LA.

Different areas will have slightly different folder structures:

> /landing/ETL/sales_oracle_ingest/customers/01DFTFX89YDFAXREPJTR94

