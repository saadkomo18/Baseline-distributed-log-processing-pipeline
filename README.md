# Distributed Log Processing Pipeline

This repository contains the baseline implementation of a scalable distributed log processing system using:

- Apache Kafka
- Apache Spark
- Ceph (MicroCeph)

The project was developed as part of a tutorial paper exploring distributed log ingestion, processing, and storage architectures.

---

## System Architecture

The system consists of three main components:

1. Kafka – log ingestion layer
2. Spark – distributed processing engine
3. Ceph – distributed storage system

Logs are generated and ingested through Kafka, processed using Spark, and stored in Ceph.

---

## Deployment Environment

The system was deployed on AWS EC2 instances.

| Component | Instance Type | CPU | RAM |
|----------|---------------|-----|-----|
Kafka | t3.large | 2 vCPU | 8 GB |
Spark | t3.large | 2 vCPU | 8 GB |
Ceph | t3.large | 2 vCPU | 8 GB |

Operating System: Ubuntu 22.04

---

## Repository Structure
kafka/ – Kafka setup scripts
spark/ – Spark analysis scripts
ceph/ – MicroCeph setup and benchmark scripts
dataset/ – sample log dataset
experiments/ – benchmark scripts
screenshots/ – experiment results


---

## Experiments

Baseline experiments were conducted to evaluate:

- Kafka ingestion throughput
- Spark log processing performance
- Ceph storage performance

Performance metrics include:

- Throughput
- Average latency
- Maximum latency

---

## Tutorial Paper

This repository accompanies the tutorial paper:

**Design and Implementation of a Scalable Distributed Log Processing Pipeline Using Apache Kafka, Apache Spark, and Ceph**

---

## Author

Saad Alshumrani