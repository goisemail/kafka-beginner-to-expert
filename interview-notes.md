# interview-notes.md — Apache Kafka Interview Preparation Notes

This document provides **concise, recall-friendly summaries** of key Kafka concepts.  
Each section contains **short bullet points (5–10 max)** designed for **quick interview revision**.  
Keep this file brief and to the point — not a detailed explanation.

---

## 🧩 Core Concepts

- Kafka is a **distributed, partitioned, replicated commit log** system.
- A **topic** is a category/feed name to which records are published.
- **Partitions** allow parallelism and scalability.
- **Producers** write data to topics; **consumers** read from them.
- Kafka provides **high throughput**, **durability**, and **fault-tolerance**.

---

## ⚙️ Producer Internals

- **acks=0,1,all** determine delivery guarantees.
- **Idempotent producers** ensure exactly-once semantics (EOS).
- Batching and compression improve throughput.
- `linger.ms` and `batch.size` tune latency vs performance.
- **Key-based partitioning** ensures ordering per key.

---

## 🧠 Consumer Internals

- Consumers join **consumer groups** for parallel consumption.
- **Offsets** track progress — auto or manual commit.
- **Rebalancing** redistributes partitions among consumers.
- `enable.auto.commit=false` gives precise control.
- Offset retention controlled by `offsets.retention.minutes`.

---

## 🧱 Kafka Internals

- Messages stored in **segment files** (append-only logs).
- **Index files** provide O(1) access by offset.
- **Retention** policy: time-based or size-based cleanup.
- **Compaction** keeps latest key-value per key.
- **ISR (In-Sync Replicas)** ensure data reliability.

---

## 🔐 Security

- Supports **SSL/TLS encryption**, **SASL** authentication.
- ACLs define access at topic/group/cluster level.
- Common mechanisms: `SASL_PLAINTEXT`, `SASL_SSL`, `SCRAM-SHA-256`.

---

## 🧩 Kafka Connect

- Framework for **data integration** — Source & Sink connectors.
- Simplifies connecting Kafka with databases and external systems.
- Configurable via REST API.
- Common connectors: JDBC, FileStream, Debezium, Elasticsearch.

---

## 🧮 Kafka Streams

- Client library for building stream-processing apps.
- Core abstractions: **KStream**, **KTable**, **GlobalKTable**.
- Stateful transformations use **state stores**.
- Provides exactly-once semantics and fault tolerance.

---

## 🏗️ Cluster Management

- **Broker**: runs Kafka server instance.
- **Controller**: manages leader election and metadata.
- **Zookeeper/KRaft**: metadata management (KRaft replacing Zookeeper).
- **Replication factor** controls fault tolerance.

---

## ⚡ Performance Tuning

- Use compression: `lz4`, `snappy` for throughput.
- Tune producer batch & linger settings.
- Optimize consumer fetch sizes.
- Use multiple partitions for parallelism.
- Monitor via JMX, Prometheus, Grafana.

---

## 🧰 Operational Topics

- **Monitoring**: lag, throughput, ISR count, disk usage.
- **Scaling**: add brokers, rebalance partitions.
- **Disaster Recovery**: MirrorMaker / MirrorMaker2 for replication.
- **Retention Policies** must match business SLAs.

---

## 🎯 Interview Quick Tips

- Understand message delivery semantics: *at-most-once, at-least-once, exactly-once*.
- Be able to explain **rebalance process** clearly.
- Know **how offsets are managed** internally.
- Understand **log compaction vs retention**.
- Be comfortable with **producer/consumer configurations** for reliability.

---

**Maintained by:** [@goisemail](https://github.com/goisemail)  
**Last updated:** 2025-10-26  
**Purpose:** Quick interview reference for Apache Kafka (not a full tutorial).
