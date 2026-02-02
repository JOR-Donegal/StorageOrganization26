# Streams as data

For most of my life I've had a standard design pattern for dealing with real time data. One process will be dedicated to ingesting the data at storing it in a suitable form: a relational database or as raw objects with metadata. Separate processes then troll through this data at rest to discern patterns of interest, further process the data, and generate alerts or reports. I liked this pattern as each component is distinct and independent. And where I'm not dealing with time critical information, this was fine. If I can accept latency between ingestion and action of for example, one second, this architecture is very scalable.

Technologies have emerged which continuously analyse data flows in real time. The dataflow itself is treated as the base store of data on which applications are built. The generic name for a platform which performed these tasks is a Streaming Data Platform (SDP). 
An SDP will normally consist of an ingestion cluster and a backing store, often called a data lake. A data lake should be able to handle any of the forms of data I have described: structured, semi structured, unstructured. You apply structure to the data when you interrogate the data lake, not when you write the data. This is called schema-on-read.

The major cloud players all have their tools for cataloguing and querying data lakes. In open source, we have had projects like Apache Hadoop for many years. As data lakes scaled like data warehouses, the term lakehouse has emerged. 

I'm hesitant to list tools, as the pace of change guarantees that by the time you read these notes they will be catastrophically out of date! But some starting points would be to read the blurb on the following Apache projects to understand what they do.

-	Apache NiFi
-	Apache Kafka

-	Apache Parquet
-	Apache ORC
-	Apache Avro

-	Apache Spark
-	Apache Flink

-	Apache Atlas
-	Apache Airflow

This is a specialist area and you could dedicate a career just to keeping current with big data processing and data lakes. In the data centre, we operate one SDP cluster with a data lake, and at time of writing, are building a second Proof of Concept (PoC) SDP. 
