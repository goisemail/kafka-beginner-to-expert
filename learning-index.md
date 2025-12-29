# learning-index.md — Apache Kafka Learning Index (Beginner → Expert)

This file defines the complete **Kafka Learning Path** from beginner to expert.  
Each numbered topic corresponds to a lesson stored under the `/lessons` directory (e.g., `lessons/01-introduction-to-kafka.md`).  
You must complete each lesson **step-by-step**, confirming before moving to the next.

---

## 🧩 LEVEL 1 — FOUNDATIONS (Beginner)

1. [**Introduction to Apache Kafka**](lessons/01-introduction-to-apache-kafka.md)
     - What is Kafka, why it exists, and common use cases
    - Core concepts overview: brokers, topics, partitions, producers, consumers

2. [**Kafka Architecture Overview**](lessons/02-kafka-architecture-overview.md)
    - Cluster, leader/follower, partitions, replicas
    - Log storage design
    - Zookeeper and KRaft (controller) overview

3. [**Kafka Setup (Local Installation)**](lessons/03-kafka-setup.md)
    - Install & configure Kafka locally (using binaries or Docker)
    - Start broker, create topics, produce and consume messages via CLI

4. [**Kafka Producer Basics (Java)**](lessons/producer/producer.md)
    - Write a simple Java producer
    - Key properties: bootstrap servers, key.serializer, value.serializer

5. [**Kafka Consumer Basics (Java)**](lessons/consumer/consumer.md)
    - Write a simple Java consumer
    - Polling, consumer groups, offsets, and auto-commit

---

## ⚙️ LEVEL 2 — INTERMEDIATE CONCEPTS

1. **Kafka Topics, Partitions & Replication**
    - Topic creation & configuration
    - Partition strategy and replica placement
    - ISR (In-Sync Replica) concept

2. **Serialization and Schema Handling**
    - Serializers/Deserializers
    - Avro, JSON, String
    - Schema Registry introduction (concept only)

3. **Consumer Groups and Rebalancing**
    - Offset management, auto-commit vs manual commit
    - Rebalancing behavior and coordination

4. **Producer Internals & Acknowledgements**
    - acks, retries, idempotence, batching, compression
    - Exactly-once delivery basics

5. **Kafka Storage Internals**
   - Log segments, index files, cleanup policies
   - Retention and compaction configuration

---

## 🧠 LEVEL 3 — ADVANCED CONCEPTS

1. **Kafka Security**
   - SSL/TLS encryption
   - SASL authentication (PLAIN, SCRAM)
   - ACL-based authorization

2. **Kafka Transactions & Exactly Once Semantics**
   - Idempotent producers
   - Transactional producers and consumers

3. **Kafka Streams (Java API)**
   - Overview of Kafka Streams library
   - Simple stream processing example

4. **Kafka Connect**
   - Source & Sink connectors
   - JDBC connector, file source/sink demo
   - Configuring connectors using REST API

5. **Kafka Monitoring and Metrics**
   - JMX metrics overview
   - Tools: Prometheus, Grafana, and Kafka Manager

---

## 🏗️ LEVEL 4 — PRODUCTION READINESS

1. **Performance Tuning**
   - Producer/consumer tuning
   - Partition strategy, compression, batching
   - Hardware and OS-level tuning

2. **Scaling Kafka Clusters**
   - Adding brokers, balancing partitions
   - Leader election and fault recovery

3. **Disaster Recovery & Multi-Cluster Setup**
   - MirrorMaker and MirrorMaker2
   - Cross-cluster replication

4. **Kafka in the Cloud**
   - Managed Kafka services (Confluent Cloud, AWS MSK, Azure Event Hubs)
   - Hybrid architectures

5. **Best Practices & Common Pitfalls**
   - Topic naming, schema evolution
   - Avoiding message loss and duplication
   - Deployment checklist

---

## 🧩 LEVEL 5 — HANDS-ON PROJECTS

1. **Mini Project 1: Event-Driven Microservice**
   - Build a Java Spring Boot microservice using Kafka for messaging

2. **Mini Project 2: Kafka Connect + Database Integration**
   - Stream data from PostgresSQL (or DB2) to another system

3. **Mini Project 3: Kafka Streams Aggregation**
   - Implement a streaming analytics pipeline

4. **Final Project: End-to-End Event Streaming System**
   - Combine producer, consumer, streams, and connectors
   - Include monitoring and fault tolerance

---

## 📘 Tracking & Progress

Use `progress.md` to track completion, notes, and reflections:

|  Level  |                                  Lesson                                  | Status | Notes |
|:-------:|:------------------------------------------------------------------------:|:------:|:-----:|
| Level 1 |   [Introduction to Kafka](lessons/01-introduction-to-apache-kafka.md)    |  Done  |       |
| Level 1 | [Kafka Architecture Overview](lessons/02-kafka-architecture-overview.md) |  Done  |       |
|         |                                                                          |        |       |

---

## 🗂 Directory Structure

Each lesson will be stored as:
