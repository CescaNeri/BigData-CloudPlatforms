# From Data Lake to Data Warehouse

**Context:** Soil moisture monitoring

Optimizing soil moisture is crucial for watering and crop performance:
The **goal** is to build an expert system to save water while improving fruit quality, having the following information:

- Soils have different water retention
- Watering systems have different behaviors 
- Plants have different water demand
- Sensors produce different measurements with different precisions

## Scenarios of DT in Agriculture

**Scenario 1:** The technician controls the watering system based on the experience, without the use of digital data / KPIs and automation.

**Scenario 2:** The control of the watering system is refined by observing sensor data (digitalized but no KPIs).

**Scenario 3:** Sensor data feeds a decision support system, knowing how to optimize KPIs, controls the watering system.

## Plan of Action

We need to understand how soil behaves.
This can be done by simulating the soil behavior according to physical models.

However, a fine tuning is required and we need to know and parametrize everything.
Tuning can take months and is extremely time consuming.

We can use **sensors** to observe the behavior of soil by observing its behavior with and without water.

![](kiwi.jpg)

They collected data for 2 years, generating 16GB of data.

## AWS

We need to create a storage space:

> Services - Storage - S3

Then, we create a bucket:

> Create Bucket

Buckets need to have a **unique name** (landing-raw-wateringsensors-789), we need to choose the location, and ACL (access control list).
Then, we can choose ti keep it public or set it private.

S3 automatically assign an id to each value, but if we add **version control**, it will also assign a *version id*, which will allow us to keep track or the versions.

**Structure:**

Ingestion pipeline -> landing -> algorithm -> staging -> algorithm

We do not need to know how the storage work, we just need to know where data are stored (**serverless service**).
It is pay-per-use, any time we move data from a bucket to another, we pay a certain amount of money.

## Load data

Load a CSV data in the bucket.

The first step is to understand the domain through **AWS sagemaker**.

> Notebook - notebook instance - create notebook instance - open Jupyter

1. Choose a name for the notebook
2. Choose the machine (ml.t3.medium)

**AWS wrangler** allows you to use AWS functionalities as if it was pandas (*maybe it is a python library*).

## Notebook

As soon as you open the jupyter notebook, it asks you to select the **kernel**.

> conda_python3

![](data.jpg)

Get rid of missing and useless data.

**Relational DataWarehouse**

```

FactTable: (timestamp, hour, date, month, year, sensor, distance, depth, value)

DT-time: (timestamp, hour, date, month, year)

DT-sensor: (sensor, dist, depth)

RELATION: (timestamp, sensor, value)

```

## Amazon RDS (Relational DB)

> Create DataBase (name: sensor-dwh, password: bigdata2022) - add public access

We added the *sensor* attribute to the DT-sensor, which serves as **primary key**.

If I have multiple fields, the primary key is not enough to identify values, we should add another attribute *field*.
But, if the DT-sensor primary key was composed just by coordinates, the additional attribute would have to be added to the domain.

By having the attribute sensor (sub-items: distance, depth, field), we can more easily model the *sensor hierarchy*, saving time, space and allowing granularity.

Once the database is created, a URL is assigned to it (sensor-dwh.cepvkrc8ii6y.us-east-1.rds.amazonaws.com).

We need to change a **security option** because we want to use Tableau for analysis (which is outside AWS), so we need to allow the communication between AWS and external entities.

> security settings - security group - inbound rules - add new rule - all traffic - source: anywhere ipv4

## Tableau

Import data from **server** (postgreSQL) - server name (sensor-dwh.cepvkrc8ii6y.us-east-1.rds.amazonaws.com), username and password.

> sheet1 - Groupby: folder

We are missing hierarchies:

> select the attributes (date, month, timestamp, year) - new folder - 

We need to create the *sensor* dimension table:

> select the attributes (depth, dist, sensor) - new folder

Then, we create a new hierarchy with *dist* and *sensor* and one with *depth* and *sensor*.
We put both hierarchies in the **sensor** folder.








