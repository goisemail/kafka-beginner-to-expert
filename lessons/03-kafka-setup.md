# Kafka Setup Guide (Zookeeper + KRaft Modes)

This guide covers both the **legacy Zookeeper-based setup** and the **modern KRaft (Kafka Raft Metadata Mode)** setup.
Use KRaft for new deployments as it removes Zookeeper and simplifies coordination.

---

## 🐳 Legacy Setup — Zookeeper Mode

Kafka depends on an **external Zookeeper service** for cluster coordination and metadata.

### 1️⃣ Create Docker Network
```bash
docker network create kafka-net
```

### 2️⃣ Run Zookeeper
```bash
docker run -d --name zookeeper --network kafka-net   -p 2181:2181 bitnami/zookeeper:latest
```

### 3️⃣ Run Kafka (Linked to Zookeeper)
```bash
docker run -d --name kafka --network kafka-net   -p 9092:9092   -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181   -e ALLOW_PLAINTEXT_LISTENER=yes   bitnami/kafka:latest
```

### 4️⃣ Verify Setup
```bash
docker ps
docker logs kafka | grep "Kafka startTimeMs"
```

### 5️⃣ Create a Topic
```bash
docker exec -it kafka kafka-topics.sh --create   --topic test-topic --bootstrap-server localhost:9092
```

### 6️⃣ Produce Messages
```bash
docker exec -it kafka kafka-console-producer.sh   --topic test-topic --bootstrap-server localhost:9092
```

### 7️⃣ Consume Messages
```bash
docker exec -it kafka kafka-console-consumer.sh   --topic test-topic --from-beginning --bootstrap-server localhost:9092
```

### 8️⃣ List Topics
```bash
docker exec -it kafka kafka-topics.sh   --list --bootstrap-server localhost:9092
```

### 9️⃣ Delete Topic
```bash
docker exec -it kafka kafka-topics.sh   --delete --topic test-topic --bootstrap-server localhost:9092
```

---

## ⚡ Modern Setup — KRaft Mode (Zookeeper-Free)

KRaft (**Kafka Raft Metadata Mode**) removes the need for Zookeeper.
Each Kafka node can act as both **Broker** and **Controller**, simplifying deployment.

### 1️⃣ Create Docker Network
```bash
docker network create kafka-net
```

### 2️⃣ Run Kafka in KRaft Mode
```bash
docker run -d --name kafka-kraft --network kafka-net   -p 9092:9092 -p 9093:9093   -e KAFKA_CFG_PROCESS_ROLES=broker,controller   -e KAFKA_CFG_NODE_ID=1   -e KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=1@localhost:9093   -e KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093   -e KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER   -e ALLOW_PLAINTEXT_LISTENER=yes   bitnami/kafka:latest
```

**Explanation:**

| Env Var                               | Description                                            |
|---------------------------------------|--------------------------------------------------------|
| `KAFKA_CFG_PROCESS_ROLES`             | Defines roles — both broker and controller.            |
| `KAFKA_CFG_NODE_ID`                   | Unique node ID in the cluster.                         |
| `KAFKA_CFG_CONTROLLER_QUORUM_VOTERS`  | Controller nodes participating in Raft quorum.         |
| `KAFKA_CFG_LISTENERS`                 | Defines ports for broker (9092) and controller (9093). |
| `KAFKA_CFG_CONTROLLER_LISTENER_NAMES` | Indicates which listener is for the controller.        |
| `ALLOW_PLAINTEXT_LISTENER`            | Enables plaintext connection (non-SSL).                |

### 3️⃣ Verify Setup
```bash
docker ps
docker logs kafka-kraft | grep "Started NetworkTrafficServerConnector"
```
You should see output similar to:
```
Started NetworkTrafficServerConnector@... on port 9092 (PLAINTEXT)
Started NetworkTrafficServerConnector@... on port 9093 (CONTROLLER)
```

### 4️⃣ Create a Topic
```bash
docker exec -it kafka-kraft kafka-topics.sh --create   --topic kraft-topic --bootstrap-server localhost:9092
```

### 5️⃣ Produce Messages
```bash
docker exec -it kafka-kraft kafka-console-producer.sh   --topic kraft-topic --bootstrap-server localhost:9092
```

### 6️⃣ Consume Messages
```bash
docker exec -it kafka-kraft kafka-console-consumer.sh   --topic kraft-topic --from-beginning --bootstrap-server localhost:9092
```

### 7️⃣ Describe the Topic
```bash
docker exec -it kafka-kraft kafka-topics.sh   --describe --topic kraft-topic --bootstrap-server localhost:9092
```

### 8️⃣ List All Topics
```bash
docker exec -it kafka-kraft kafka-topics.sh   --list --bootstrap-server localhost:9092
```

### 9️⃣ Delete a Topic
```bash
docker exec -it kafka-kraft kafka-topics.sh   --delete --topic kraft-topic --bootstrap-server localhost:9092
```

---

## 🧱 Optional — Multi-Broker KRaft Setup

| Container | Broker Port | Controller Port |
|-----------|-------------|-----------------|
| kafka-1   | 9092        | 9093            |
| kafka-2   | 9094        | 9095            |
| kafka-3   | 9096        | 9097            |

Each broker needs:
```bash
-e KAFKA_CFG_NODE_ID=<unique_id>
-e KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=1@kafka-1:9093,2@kafka-2:9095,3@kafka-3:9097
```

---

## 💡 Comparison Summary

| Feature            | Zookeeper Setup           | KRaft Setup                    |
|--------------------|---------------------------|--------------------------------|
| Coordination       | External (Zookeeper 2181) | Internal (Raft quorum 9093+)   |
| Services           | 2 (Zookeeper + Kafka)     | 1 (Kafka only)                 |
| Startup Complexity | Higher                    | Simpler                        |
| Metadata Storage   | Zookeeper nodes           | Raft metadata log              |
| Leader Election    | Via Zookeeper             | Internal Raft consensus        |
| Introduced         | Legacy (pre-2.8)          | Kafka 2.8+ (default ≥3.5)      |
| Recommended        | ❌ Deprecated              | ✅ Preferred                    |

---

## 🧠 Notes

- **KRaft is the future of Kafka**; Zookeeper mode will be deprecated.  
- **Single-node KRaft** is fine for local testing.  
- For production, use **3+ controller nodes** for quorum safety.  
- All client tools (`kafka-topics.sh`, `kafka-console-producer.sh`, `kafka-console-consumer.sh`) work the same in both modes.

---

**End of Kafka Setup (Zookeeper + KRaft)**  
