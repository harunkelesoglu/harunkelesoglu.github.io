---
layout: post
usehighlight: false
tags: [apache-kafka, kafka-best-practices,kafka-performance-improvements]
title: An In-Depth Look at Kafka, Some Performance Improvements
---

### 1. **Introduction**

Kafka is a robust and low-latency broker widely preferred in most event-driven architectures. This notes explains the fundamental architecture, components,structure and performance improvements of Kafka.

### 2. **Core API**

#### 2.1 **Producer API**

**Producer:**
The Producer API is used to publish (write/produce) messages to Kafka topics. Producers can be configured with various parameters, including Kafka broker addresses, message key and value serializers, and more. They automatically handle the partitioning of messages across different partitions in a topic.

**Message:**
A message produced by a producer typically consists of a key and a value. The key is optional, and the value contains the actual data. Messages are sent to Kafka topics, which are logical channels or feeds where messages are published.

**Partitioning:**
Producers can optionally provide a key when sending a message, and Kafka uses this key to determine the partition to which the message should be written. Custom partitioning strategies can be implemented, or Kafka can use the default partitioning logic.

**Acknowledgments:**
Producers can be configured to receive acknowledgments (acks) from Kafka brokers, indicating whether the message was successfully written to the broker.

#### 2.2 Consumer API

**Consumer:**
The Consumer API is used to subscribe to Kafka topics and read (consume) messages from those topics. Consumers can be part of a consumer group, allowing multiple consumers to work together to consume messages from a set of partitions.

**Consumer Groups:**
Consumers within the same consumer group divide the partitions of a topic among themselves to achieve parallelism. Kafka ensures that each partition is consumed by only one consumer within a consumer group, ensuring a single processing order for each partition.

**Offset Management:**
Kafka maintains the offset, a unique identifier for each message within a partition. Consumers are responsible for tracking and managing their current offset in the topic. When consuming messages, Kafka knows where it left off by checking this offset value.

**Commit and Auto-commit:**
Consumers can manually commit offsets or enable auto-commit, allowing Kafka to automatically manage offsets at specific intervals.

**Polling:**
Consumers poll Kafka for new messages. The `poll()` method is used to retrieve batches of messages from Kafka.

![Consumer Group](/assets/svg/consumer.group-offset.svg)


### 3. Fundamental Architecture of a Broker

* **Topic:**
  - A topic is like a database in Kafka. Producer delivers data to a topic, and consumers consume data from the topic.
* **Partition:**
  - The smallest unit in Kafka. A topic is divided into several parts known as partitions. These partitions are separated in a specific order. The content of the data is stored in the partitions within the topic, and the data written to a partition can never be changed; it is immutable.
* **Offset:**
  - Each message in a partition is assigned a unique offset, which is an incremental ID. This offset helps Kafka track the position of the consumer within a partition.
* **Broker:**
  - A fundamental component serving as a message broker or message server. Brokers manage the storage, distribution, and retrieval of messages in a Kafka cluster. Kafka brokers are known as bootstrap brokers because a connection with any one broker means connection with the entire broker in the cluster.

  ![Kafka Broker Architecture](/assets/svg/kafka-broker.svg)


#### 3.1 Important Considerations

* **Append-Only:**
  - Kafka follows an append-only storage mechanism. Once a message is written to a partition, it is immutable, and the data cannot be modified.
* **Retention:**
  - Kafka retains messages in partitions for a configurable retention period. After this period, messages can be automatically deleted.
* **Replication:**
  - For fault tolerance, each partition has multiple replicas distributed across different brokers, ensuring data accessibility even if a broker or partition becomes unavailable.

#### 3.2 Partition Assignment Strategy

In Kafka, the distribution of topics and partitions across brokers is determined by the partition assignment strategy. By default, Kafka uses a simple round-robin assignment strategy.


For example, if you have three topics and three brokers, the partitions for each topic will be distributed across the available brokers:

- Broker 1: Topic1-Partition1, Topic2-Partition1, Topic3-Partition1
- Broker 2: Topic1-Partition2, Topic2-Partition2, Topic3-Partition2
- Broker 3: Topic1-Partition3, Topic2-Partition3, Topic3-Partition3

This distribution allows Kafka to take advantage of available resources on each broker, providing fault tolerance as replicas of partitions can be stored on other brokers.

![Kafka Fault Tolerance](/assets/svg/fault-tolerance.svg)

### 4. Delivery Semantic

There are three main delivery semantics in Kafka:

* **At Most Once (Fire and Forget):**
  - Messages are sent to the broker, and once the broker acknowledges receipt, the producer assumes the message is delivered. However, there is no guarantee that the message will be successfully processed, and it might be lost if an issue occurs after acknowledgment.

* **At Least Once (Guaranteed Delivery):**
  - Messages are sent to the broker, and the producer waits for an acknowledgment from the broker before considering the message delivered. If an acknowledgment is not received, the producer retries sending the message. This ensures that the message is delivered at least once, but it may be processed multiple times.

* **Exactly Once (Transactional Delivery):**
  - The most advanced and strict semantic, guaranteeing that a message is delivered exactly once, not lost, and not processed more than once. Kafka achieves this through the use of transactions, where the producer can send a batch of messages along with metadata in a single transaction. Consumers then read messages from a committed transaction, ensuring both message durability and single processing.

### 5. ZooKeeper

ZooKeeper is an open-source distributed coordination service often used in conjunction with Apache Kafka to manage and coordinate distributed systems. No Kafka server can run without ZooKeeper. It provides coordination, synchronization, and distributed management services for Kafka's distributed environment. Specifically, ZooKeeper serves several key purposes within a Kafka cluster:

- **Metadata Management:** ZooKeeper manages and stores metadata related to the Kafka cluster, including information about brokers, topics, partitions, and the current state of the cluster.
- **Leader Election:** Kafka relies on ZooKeeper for leader election in a partition. Each partition in Kafka has one leader broker responsible for handling reads and writes. ZooKeeper helps in the election process to ensure that a new leader is selected if the current leader fails.
- **Broker Registration:** Kafka brokers register themselves in ZooKeeper, allowing other components (producers and consumers) to discover and communicate with available brokers.
- **Cluster Coordination:** ZooKeeper coordinates the actions of different brokers in the Kafka cluster, ensuring they have a consistent view of the cluster state. This coordination is essential for maintaining the overall health and stability of the Kafka environment.
- **Notification and Watch Mechanism:** ZooKeeper provides a notification and watch mechanism that Kafka components can leverage to be notified of changes in the cluster, such as the addition or removal of brokers or changes in topic configurations.
- **Configuration Management:** ZooKeeper is used to store and manage configuration information for Kafka, including details about topic configurations, consumer group offsets, and other runtime configurations.

 ![Zookeeper](/assets/svg/zookeeper.svg)


### 6. Advantages & Disadvantages of Kafka

**Advantages:**
- **Low Latency:** Kafka offers low-latency processing, with values as low as 10 milliseconds.
- **High Throughput:** Kafka can handle a large number of messages with high volume and velocity.
- **Fault Tolerance:** Kafka can continue to consume and produce messages even if some brokers go down, provided it is configured accordingly.
- **Durability:** Messages in Kafka are durable, ensuring data persistence.
- **Flexibility:** Kafka reduces complexity, enabling easy integration with any system using producers and consumers.
- **Distributed Architecture:** Kafka features a distributed architecture that enhances scalability through partitioning and replication.
- **Real-time Handling:** Kafka is capable of handling real-time data pipelines, including processors, analytics, and storage.

**Disadvantages:**
- **No Wildcard Support in Topics:** Kafka does not support wildcard functionality in topic subscriptions.
- **Clumsy Behavior:** Kafka may exhibit clumsy behavior, especially when the number of topics increases in the cluster.
- **Limited Monitoring Tools:** Kafka lacks a complete set of monitoring tools.

### 7. Kafka Performance Improvements

#### 7.1 Disks I/O

- Kafka reads and writes data sequentially due to its log-centric architecture. Choose a disk type (HDDs or SSDs) that aligns well with Kafka's sequential access patterns.
- Choosing XFS as the file system for the drives where Kafka data is stored can be beneficial for performance. Drives should be formatted as XFS, which efficiently handles large amounts of data and concurrent operations, optimizing for high-throughput workloads.
- If read/write throughput is your bottleneck, mount multiple disks in parallel for Kafka.
- Kafka's performance is directly proportional to the amount of data. Setting the retention of stored data as low as possible will reduce disk usage.

#### 7.2 Network

- Kafka instances and ZooKeeper instances should be geographically close.
- Bandwidth is crucial for Kafka due to its nature as a distributed streaming platform that handles large volumes of data in real-time.

#### 7.3 RAM / JAVA Heap

- A minimum of 8GB RAM is required for brokers, but 16 or 32GB will be more suitable.
- Do not set -Xms for starting heap size. Set a maximum heap size (-Xmx) to ensure Kafka has enough memory resources.
```bash
    export KAFKA_HEAP_OPTS="-Xmx4G" 
```
- Make sure swapping is disabled for Kafka entirely (`vm.swappiness=0`, `vm.swappiness=1`).

#### 7.4 CPU

CPU is usually not a performance bottleneck in Kafka because Kafka does not parse any messages, but it can become one in some situations.
- If you have SSL enabled, Kafka has to encrypt and decrypt every payload, which adds load on the CPU. Move Kafka to VPC and disable SSL.

### 8. Some important configurations

```bash
# Number of threads dedicated to handling background tasks
# Increase in scenarios of high load, a large number of topics/partitions, or disk I/O intensity
background.threads=10

# Number of messages triggering a log flush
# Increase if more frequent log flushes are required, decrease for larger batches before a flush
log.flush.interval.messages=

# Retention period for log segments in hours
# Increase to retain log segments for a longer period
log.retention.hours=168

# Maximum size allowed for a single Kafka message in bytes
# Increase when dealing with larger messages, mindful of broker and network capacity
message.max.bytes=1000012

# Number of I/O threads for handling disk operations
# Increase in scenarios of high disk I/O
num.io.threads=3

# Number of network threads per data directory
# Increase if there's a high network load
num.network.threads.per.data.dir=1

# Number of fetcher threads used to replicate data between brokers
# Increase in scenarios with high replication demand
num.replica.fetchers=1

# Enable or disable unclean leader election
# Set to true if high availability is a priority and data loss can be tolerated
unclean.leader.election.enable=true

# ZooKeeper session timeout in milliseconds
# Increase if ZooKeeper connections are timing out
zookeeper.session.timeout.ms=6000

# Rack location of the broker (null indicates no specific rack)
# Increase if implementing rack awareness, set to the appropriate rack location
broker.rack=null

# Default replication factor for topics
# Increase for higher fault tolerance, but it affects resource usage
default.replication.factor=1

# Default number of partitions for a topic
# Increase when creating new topics, based on expected workload and parallelism requirements
num.partitions=1
```
