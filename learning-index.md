# learning-index.md — Apache Kafka Learning Index (Beginner → Expert)

This file defines the complete **Kafka Learning Path** from beginner to expert.  
Each numbered topic corresponds to a lesson stored under the `/lessons` directory (e.g., `lessons/01-introduction-to-kafka.md`).  
You must complete each lesson **step-by-step**, confirming before moving to the next.

---

## 🧩 LEVEL 1 — FOUNDATIONS (Beginner)

1. **Introduction to Apache Kafka**
    - What is Kafka, why it exists, and common use cases
    - Core concepts overview: brokers, topics, partitions, producers, consumers

2. **Kafka Architecture Overview**
    - Cluster, leader/follower, partitions, replicas
    - Log storage design
    - Zookeeper and KRaft (controller) overview

3. **Kafka Setup (Local Installation)**
    - Install & configure Kafka locally (using binaries or Docker)
    - Start broker, create topics, produce and consume messages via CLI

4. **Kafka Producer Basics (Java)**
    - Write a simple Java producer
    - Key properties: bootstrap servers, key.serializer, value.serializer

5. **Kafka Consumer Basics (Java)**
    - Write a simple Java consumer
    - Polling, consumer groups, offsets, and auto-commit

---

## ⚙️ LEVEL 2 — INTERMEDIATE CONCEPTS

6. **Kafka Topics, Partitions & Replication**
    - Topic creation & configuration
    - Partition strategy and replica placement
    - ISR (In-Sync Replica) concept

7. **Serialization and Schema Handling**
    - Serializers/Deserializers
    - Avro, JSON, String
    - Schema Registry introduction (concept only)

8. **Consumer Groups and Rebalancing**
    - Offset management, auto-commit vs manual commit
    - Rebalancing behavior and coordination

9. **Producer Internals & Acknowledgements**
    - acks, retries, idempotence, batching, compression
    - Exactly-once delivery basics

10. **Kafka Storage Internals**
    - Log segments, index files, cleanup policies
    - Retention and compaction configuration

---

## 🧠 LEVEL 3 — ADVANCED CONCEPTS

11. **Kafka Security**
    - SSL/TLS encryption
    - SASL authentication (PLAIN, SCRAM)
    - ACL-based authorization

12. **Kafka Transactions & Exactly Once Semantics**
    - Idempotent producers
    - Transactional producers and consumers

13. **Kafka Streams (Java API)**
    - Overview of Kafka Streams library
    - Simple stream processing example

14. **Kafka Connect**
    - Source & Sink connectors
    - JDBC connector, file source/sink demo
    - Configuring connectors using REST API

15. **Kafka Monitoring and Metrics**
    - JMX metrics overview
    - Tools: Prometheus, Grafana, and Kafka Manager

---

## 🏗️ LEVEL 4 — PRODUCTION READINESS

16. **Performance Tuning**
    - Producer/consumer tuning
    - Partition strategy, compression, batching
    - Hardware and OS-level tuning

17. **Scaling Kafka Clusters**
    - Adding brokers, balancing partitions
    - Leader election and fault recovery

18. **Disaster Recovery & Multi-Cluster Setup**
    - MirrorMaker and MirrorMaker2
    - Cross-cluster replication

19. **Kafka in the Cloud**
    - Managed Kafka services (Confluent Cloud, AWS MSK, Azure Event Hubs)
    - Hybrid architectures

20. **Best Practices & Common Pitfalls**
    - Topic naming, schema evolution
    - Avoiding message loss and duplication
    - Deployment checklist

---

## 🧩 LEVEL 5 — HANDS-ON PROJECTS

21. **Mini Project 1: Event-Driven Microservice**
    - Build a Java Spring Boot microservice using Kafka for messaging

22. **Mini Project 2: Kafka Connect + Database Integration**
    - Stream data from PostgreSQL (or DB2) to another system

23. **Mini Project 3: Kafka Streams Aggregation**
    - Implement a streaming analytics pipeline

24. **Final Project: End-to-End Event Streaming System**
    - Combine producer, consumer, streams, and connectors
    - Include monitoring and fault tolerance

---

## 📘 Tracking & Progress

Use `progress.md` to track completion, notes, and reflections:
| Level | Lesson | Status | Notes |
|--------|---------|---------|-------|
| Level 1 | Introduction to Kafka | ☐ | |
| Level 1 | Kafka Architecture Overview | ☐ | |
| ... | ... | ... | ... |

---

## 🗂 Directory Structure

Each lesson will be stored as:
