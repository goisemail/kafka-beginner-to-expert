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

## 📘 Kafka vs RabbitMQ / System Design and I/O Internals

**Architecture Type**
- Kafka = Distributed Commit Log; RabbitMQ = Message Broker Queue.

**Message Flow Model**
- Kafka = **Pull-based** — consumers poll brokers at their own pace.  
- RabbitMQ = **Push-based** — broker delivers messages automatically via AMQP.

**Protocols**
- Kafka → Binary TCP protocol on port 9092.  
- RabbitMQ → AMQP (Advanced Message Queuing Protocol) on port 5672.

**Acknowledgment**
- Kafka → Consumers commit offsets to track progress.  
- RabbitMQ → Consumers send ACK/NACK responses.

**Storage & Durability**
- Kafka → Persisted on disk (append-only log); messages retained after consumption → supports replay, auditing, and recovery.  
- RabbitMQ → Typically transient (queue empties after ACK).

**Performance Internals**
- Kafka uses **sequential writes** (no random I/O) → high throughput.  
- Utilizes **zero-copy transfer (sendfile)** → kernel to network without user-space copy.  
- Uses **page cache batching** and **compression** for performance.  

**Cluster Coordination**
- Managed by **Zookeeper** (legacy) or **KRaft** (modern controller quorum).  

**Hardware Profile**
- Runs on **commodity servers** (standard hardware) yet scales to millions of messages per second.  

**Key Terms**
- **Broker** = Kafka server storing topic partitions.  
- **Partition** = Append-only log file.  
- **Offset** = Consumer’s bookmark.  
- **Retention Policy** = Controls data lifecycle, not consumption.

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

- Kafka is **pull-based**, RabbitMQ is **push-based**.  
- Kafka retains data post-consumption → supports **replay, auditing, and recovery**.  
- Sequential disk writes + zero-copy I/O = **high throughput**.  
- Kafka = binary TCP protocol; RabbitMQ = AMQP.  
- Commodity hardware can support massive throughput.  
- Coordination via Zookeeper/KRaft ensures partition leadership and fault tolerance.  
- Ideal for event-driven microservices and streaming pipelines.  
- Understand message delivery semantics: *at-most-once, at-least-once, exactly-once.*  
- Be able to explain **rebalance process** clearly.  
- Know **how offsets are managed** internally.  
- Understand **log compaction vs retention**.  
- Be comfortable with **producer/consumer configurations** for reliability.

---

**Maintained by:** [@goisemail](https://github.com/goisemail)  
**Last updated:** 2025-10-26  
**Purpose:** Quick interview reference for Apache Kafka (not a full tutorial).
