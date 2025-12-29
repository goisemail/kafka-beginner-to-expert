### Kafka Producers
## Key Concepts:
 - Messages: Producers send messages (records) to Kafka topics.
 - Partitions: Producers can choose which partition to send messages to within a topic.
 - Acknowledgment: Producers can specify the level of acknowledgment required for sent messages.
 - Batching: Producers can batch multiple messages together for efficient sending.


## Producer Configuration Options:
- Bootstrap Servers: A list of Kafka broker addresses that the producer uses to connect to the Kafka cluster.
- Key and Value Serialization: Producers must serialize the keys and values of messages before sending them.
- Partitioner: Determines how the producer chooses a partition for each message.
- Acks: Determines the level of acknowledgment required. Options include:
  - 0: No acknowledgment required.
  - 1: Acknowledge after the message is received by the leader partition.
  - all: All in-sync replicas must acknowledge the message.
- Retries: Number of retry attempts for failed sends.
