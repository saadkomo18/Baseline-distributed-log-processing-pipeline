
# Scalable Distributed Log Processing Pipeline

This repository contains the **baseline implementation** of a distributed log processing system developed for the tutorial paper:

**"Design and Implementation of a Scalable Distributed Log Processing Pipeline Using Apache Kafka, Apache Spark, and Ceph."**

The project demonstrates the deployment and evaluation of three core distributed systems technologies:

- Apache Kafka – log ingestion
- Apache Spark – distributed log processing
- Ceph (MicroCeph) – distributed storage

The goal is to provide a **reproducible baseline implementation** before integrating the full pipeline.

---

# System Architecture

The baseline architecture evaluates each technology independently.

Log Generator → Kafka → Spark Processing → Ceph Storage

Kafka handles log ingestion, Spark performs distributed log analysis, and Ceph provides scalable storage.

---

# Deployment Environment

The experiments were conducted on **AWS EC2 instances** using the following configuration:

| Component | Instance Type | vCPU | Memory | Storage |
|-----------|---------------|------|--------|--------|
| Kafka Node | t3.large | 2 | 8 GB | 50 GB |
| Spark Node | t3.large | 2 | 8 GB | 50 GB |
| Ceph Node | t3.large | 2 | 8 GB | 50 GB |

Operating System: **Ubuntu 22.04 LTS**

---

# Repository Structure

distributed-log-processing-pipeline
│
├── kafka
│   ├── kafka_setup.sh
│   ├── create_topic.sh
│
├── spark
│   ├── spark_log_analysis.scala
│   ├── run_spark_job.sh
│
├── ceph
│   ├── microceph_setup.sh
│   ├── ceph_benchmark.sh
│
├── dataset
│   └── logs.txt
│
├── experiments
│   └── kafka_benchmark.sh
│
└── screenshots

---

# Kafka Baseline Experiment

Kafka was deployed in standalone mode using the KRaft consensus mechanism.

### Create Topic

bin/kafka-topics.sh --create \
--topic logs \
--bootstrap-server localhost:9092 \
--partitions 3 \
--replication-factor 1

### Producer Benchmark

bin/kafka-producer-perf-test.sh \
--topic logs \
--num-records 100000 \
--record-size 100 \
--throughput 5000 \
--producer-props bootstrap.servers=localhost:9092

---

# Spark Baseline Experiment

Spark was executed in **local standalone mode**.

### Run Spark Shell

spark-shell --master local[*]

### Log Analysis Example

val logs = sc.textFile("file:///home/ubuntu/biglogs.txt")

val errors = logs.filter(_.contains("ERROR"))

val count = errors.count()

println("ERROR count = " + count)

---

# Ceph Baseline Experiment

A single-node **MicroCeph deployment** was used to validate distributed storage functionality.

### Create Storage Pool

sudo microceph.ceph osd pool create logpool 32

### Storage Benchmark

sudo microceph.rados bench -p logpool 60 write --no-cleanup

---

# Dataset

A synthetic dataset of log entries was generated for testing.

Example log entry:

2026-02-23 21:30:01 [INFO] (auth-service) User login successful
2026-02-23 21:30:02 [ERROR] (database) Connection timeout detected

---

# Tutorial Paper

This repository accompanies the tutorial paper submitted as part of a research project on scalable log processing systems.

---

# Author

Saad Alshumrani  
