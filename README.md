# Real-Time Log Processing Pipeline with Kafka, Flume, HDFS & Spark

##  Project Overview

This project demonstrates a real-time data pipeline for ingesting, storing, and processing Apache web server logs using open-source big data tools. It simulates live log streaming using a log generator, ingests logs using Apache Flume, publishes to Kafka, stores data in HDFS, and analyzes the logs using PySpark.

---

##  Architecture Overview

![WhatsApp Image 2025-05-05 at 09 38 51_c8fb466f2](https://github.com/user-attachments/assets/4f7f544b-6992-4e84-b22e-83f81b22e7f6)

---

##  Components

### 1. Logs Generator
- `Logs_generator.py` & `NASA_logs_generator.py`
- Simulates log traffic by downloading NASA web server logs.
- Sends logs line-by-line over a socket to Flume.

### 2. Flume Configurations
- `flume_kafka.conf`: Receives logs from netcat and forwards to Kafka.
- `flume_from_kafka.conf`: Consumes logs from Kafka and writes to HDFS.

### 3. Kafka
- Used as a real-time message broker between Flume agents.

### 4. HDFS
- Stores raw log data streamed from Kafka via Flume.

### 5. PySpark Notebook
- `pyspark_streaming.ipynb`: Analyzes the logs using PySpark.
- Example analyses include traffic volume, error rates, and request types.

---

##  How to Run the Project

1. **Start Kafka and Zookeeper**

   ```bash
   bin/zookeeper-server-start.sh config/zookeeper.properties
   bin/kafka-server-start.sh config/server.properties
   ```
2. **Start Flume Agent for Netcat → Kafka**
   ```bash
   flume-ng agent --conf ./conf --conf-file ./conf/flume_kafka.conf --name agent -Dflume.root.logger=INFO,console

   ```
3. **Run the Logs Generator**
   ```bash
   python NASA_logs_generator.py


   ```
4. **Start Flume Agent for Kafka → HDFS**
   ```bash
   flume-ng agent --conf ./conf --conf-file ./conf/flume_from_kafka.conf --name agent -Dflume.root.logger=INFO,console

   ```

5. **Run PySpark Notebook**
