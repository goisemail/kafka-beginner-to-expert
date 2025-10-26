### Kafka Consumers

## Key Concepts:
- Consumer Groups: Consumers can belong to a group, allowing for distributed processing of topic data across multiple consumers.
- Offsets: Consumers keep track of their position in each partition using offsets.
- Re-balancing: When consumers join or leave a group, Kafka re-balances the partitions among the group members.

## Consumer Configuration Options:
- Bootstrap Servers: A list of Kafka broker addresses that the consumer uses to connect to the Kafka cluster.
- Group ID: An identifier for the consumer group.
- Auto Offset Reset: Determines what happens when a consumer has no offset (either never read the partition or lost its offset data):
  - earliest: Start from the earliest available message.
  - latest: Start from the latest available message.
  - Enable Auto Commit: Automatically commits offsets at regular intervals.
