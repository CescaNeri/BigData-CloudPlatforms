# Technogym - Data Analytics Pipeline

Technogym is the leader for the market of sports equipment. As of today, they are not selling equipment, but they are selling solutions. They provide digital platform that allows users to connect.

They sell **digital services** to costumers who can access via smartphone.

## Technogym Data

Data is essential fot digital transformation.
When we talk about data pipeline, we refer to the entire process of data collection and analysis.

It starts with data capture with data ingestion at any scale, then data is processes, stored in DL and DW, analyzed and used.
Technogym uses Google Cloud as PaaS.

**Data Pipeline:**

Through the use of Paas, technogym is able to perform advances analytics on data without coding.

## IoT

A distributed system in which objects in the physical world are connected to the internet.

*Where does data of technogym come from?*

IoT is enabled by ubiquitous, low-cost internet connectivity with high speed and bandwidth.

The outcome of IoT is the availability of huge quantity of data. Every year the humanity produces more and more data.

**Raw Data types:**

- Status data
- Time-series data
- Location data
- Images, videos and files

Data can be captured and ingested in different modalities, according to:

- Small data size
- Frequency of communication different from device to device
- Direction of communication (in some cases communication needs to be bi-directional)

**Key Qualities for Storage:**

- Availability 
- Durability
- Reliability
- Fault Tolerance (zero downtime)
- Consistency (data integrity)

## Google BigQuery

How do they choose where to locate the machines?

1. Regulations (keep data in Europe)
2. Where data is needed

```sql
SELECT JSON_EXTRACT(data) AS RawData
WHERE DATE(publish_time) = "2022-12-05"
```

BigQuery gives you the possibility to **schedule queries**, so that you can set a query to run automatically at pre-set times.

**Google DataStudio** performs the same jobs as Tableau.

BigQuery understands the data type that you are dealing with and allows you to work with the data without the need to convert it.

## SQL case

```sql
CREATE view file_name/view
SELECT TimeStampEvent, JSON_VALUE(jsondata.data.message.data) as counter
FROM file_name/json
WHERE JSON_VALUE(jsondata.data.message.data) IS NOT NULL
```

To display data on an excel file, we just need to open a new google sheet file and open the view we created.

Alternatively, queries can be directly written on google sheets when you open the data.

We can select `refresh` options which allow us to schedule refresh times.

## BigQuery ML

As soon as you have data on BigQuery, BigQuery ML allows you to build ML models without the need of extracting the data first.

With BigQuery ML, there is no need to use python or java, but you can just use SQL. 
You can choose among different models like linear regression, K-means and so on.

`AutoML` allows developers with limited machine learning experience to train high-quality models specific to their business needs.

