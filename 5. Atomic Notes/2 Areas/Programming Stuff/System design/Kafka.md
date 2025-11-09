2025-07-21 21:13
Status: #baby
Tags: [[system design]]
## Main

### What? 
Kafka is a **distributed streaming platform** developed by **Apache Software Foundation**. It’s used to build **real-time data pipelines and streaming applications**. In simple terms, Kafka is like a **messaging system**, but highly scalable, fast, and fault-tolerant.

| Term                             | Description                                                                                                                                    |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Topic**                        | A named stream of data where messages are written by producers and read by consumers. Think of it like a category or a "channel" for messages. |
| **Producer**                     | A client or service that sends (publishes) data/messages to Kafka topics.                                                                      |
| **Consumer**                     | A client or service that reads (subscribes to) messages from Kafka topics.                                                                     |
| **Consumer Group**               | A group of consumers working together to read messages from a topic. Each message is read by only one consumer in the group.                   |
| **Broker**                       | A Kafka server that stores topic data and handles requests from producers and consumers. Kafka runs as a cluster of these brokers.             |
| **Partition**                    | A topic can be split into partitions for parallelism. Each partition is an ordered sequence of messages.                                       |
| **Offset**                       | A unique ID for each message within a partition. It helps Kafka keep track of what has been consumed.                                          |
| **ZooKeeper** _(legacy)_         | A service Kafka used to rely on for managing the cluster metadata (though Kafka is now moving away from it with **KRaft mode**).               |
| **Retention**                    | How long Kafka keeps messages in a topic, even after they're read. Useful for replaying data.                                                  |
| **Replication Factor**           | The number of copies of a partition stored on different brokers for fault tolerance.                                                           |
| **Leader** / **Follower**        | In each partition, one broker is the "leader" and handles reads/writes. The others are "followers" that replicate the data.                    |
| **Kafka Cluster**                | A group of brokers working together to manage and distribute data.                                                                             |
| **Kafka Connect**                | A tool for integrating Kafka with external systems (e.g., databases, cloud storage) via connectors.                                            |
| **Kafka Streams**                | A library for building real-time processing and analytics apps on top of Kafka.                                                                |
| **Schema Registry**              | A system (e.g., from Confluent) that manages data schemas, ensuring message format compatibility.                                              |
| **Exactly Once Semantics (EOS)** | Guarantees that a message is processed only once — not lost, not duplicated (requires special config).                                         |


### Acks 
#### Producer

| `acks` Value | Who Acknowledges | Performance | Durability |
| ------------ | ---------------- | ----------- | ---------- |
| `0`          | No one           | 🟢 Fastest  | 🔴 Risky   |
| `1`          | Leader only      | 🟡 Medium   | 🟡 Medium  |
| `all` / `-1` | All replicas     | 🔴 Slowest  | 🟢 Strong  |
✅ acks=0
No acknowledgements.

Producer doesn’t wait for any response.

Fastest, but not reliable.

Messages may be lost if the broker crashes.

✅ acks=1
Kafka broker’s leader partition confirms receipt.

The producer gets an ack only from the leader.

Balanced in performance and reliability.

If the leader crashes before replication, data may be lost.

✅ acks=all (or acks=-1)
The leader waits for all replicas (followers) to acknowledge the write.

Strongest durability guarantee.

Slowest of the three, but safest for critical data.

acks=0: High-speed logs that aren’t critical (e.g. debug info).

acks=1: Balanced use case (e.g. normal transactions).

acks=all: Financial data, orders, critical business events.

#### Consumer

✅ **Consumer Acknowledgement = Offset Commit**

|Commit Mode|Trigger|Acknowledgement Style|Pros|Cons|
|---|---|---|---|---|
|Auto|Timer|Kafka handles it|Easy|Risk of loss|
|Manual Sync|Code|You handle, wait for response|Reliable|Slower|
|Manual Async|Code|You handle, no waiting|Fast|Less safe|
### 🧠 Key Concept:

> **Kafka consumer acknowledgement is not a message-level “ACK”** — it’s **partition-offset-level tracking**.

This means:

- **Kafka doesn’t acknowledge each message individually** (like "Message 1: ACK", "Message 2: ACK").
    
- Instead, it tracks **how far the consumer has gotten in a partition** — using an **offset number**.
    

So the consumer is basically saying:

> "I've successfully processed messages **up to this offset** in this partition. If I stop or restart, resume from here."

| Feature              | Kafka                       | RabbitMQ / MQ   |
| -------------------- | --------------------------- | --------------- |
| Acknowledgement type | **Offset (per partition)**  | **Per message** |
| Replay old messages? | ✅ Yes (with offset control) | ❌ Not easily    |
| Model                | Pull-based                  | Push-based      |
| Durability control   | Consumer-controlled         | Broker-enforced |
###  Commit strategy
A **commit strategy** determines:

- **When** a consumer saves its position (offset) in the topic.
    
- **How** it saves it (automatically or manually).
    
- This affects **message reliability**, **performance**, and **duplicate/replay risks**.
#### Auto commit
🔁 Automatic Commit (default)
Enabled by: enable.auto.commit=true
Kafka automatically commits offsets at regular intervals:
auto.commit.interval.ms (default = 5000 ms)
🔹 Pros:
Simple to use
Minimal code
🔸 Cons:
Risk of message loss: offset may be committed before message is fully processed
Not good for critical systems
#### 🛠 Manual Commit

### Error Handling Strategies
#### 1. Retry + Dead Letter Queue (DLQ)
- Retry a few times.
- If still failing, move the record to a **Dead Letter Topic** (DLQ) for later inspection.
#### 2. Skip & Log (Ignore Strategy)**
- Log the error.
- Skip the record (no retry).
- Commit the offset anyway.
#### 3. Pause / Resume Consumption**
Kafka lets you pause consuming from a partition while you deal with an error.
✅ Useful for:

- Temporary downstream issues
    
- Avoiding re-polling while you retry or clean up
#### 4. Fail Fast**
Crash the application if a critical error occurs.

✅ Good for:

- Systems where **data integrity is more important** than uptime
    
- You rely on a supervisor or container (like Kubernetes) to restart
#### 5. Catch & Commit Carefully
Catch exceptions and **only commit offsets if the record was processed** successfully.

#### Last-Resort Strategies for Irrecoverable Messages
```
## 🔁 Why This Happens

You're likely doing one of the following:

- You **re-process the DLQ message** with the **same broken logic**.
    
- You **re-send** it to the DLQ again (accidentally).
    
- You **don’t track how many times it's been retried**, so it just goes in circles.
    
- You **don’t isolate DLQ processing** from the original pipeline.
    

This creates a **retry loop hell** or **zombie message loop**.

---

## ✅ Solution: Break the Infinite Retry Loop

### 🧱 1. **Make DLQ a Terminal Point**

- DLQ is **not** meant to be retried automatically in most setups.
    
- Treat it like a **dead-end** unless someone **manually inspects and repairs** the message.
    

### 💡 2. **Tag or Track Retry Attempts**

Add a retry header to the message (e.g., `x-retry-count`) and **increment it** each time the message is processed:

java

Sao chépChỉnh sửa

`int retries = headers.getOrDefault("x-retry-count", 0); if (retries > MAX_RETRIES) {     sendToPermanentFailureTopic(message);     return; }`

This way, you can stop after a threshold (e.g., 3 attempts total).

### 🧯 3. **Use a Separate DLQ Processor**

Your DLQ consumer should be:

- Separate from your main logic
    
- Ideally with **more safety checks**, logging, and manual gating
    
- Possibly only active under **manual trigger**
    

text

Sao chépChỉnh sửa

`Main Consumer → DLQ DLQ Consumer → Log / Store / Alert (no more DLQ!)`

### 🛑 4. **Never Write DLQ Back to Itself**

Make sure you don't accidentally do this:

java

Sao chépChỉnh sửa

`catch (Exception e) {     producer.send("dlq", message); // 🚫 don’t do this blindly in DLQ consumer! }`

If your DLQ consumer fails again, **log the error and stop** or move to a permanent-dead-letter topic.

---

## 🛠️ Example Strategy

java

Sao chépChỉnh sửa

`try {     process(message); } catch (Exception e) {     int retryCount = getRetryHeader(message);     if (retryCount >= 3) {         sendToPermanentFailureTopic(message);     } else {         sendToRetryTopic(message, retryCount + 1);     } }`

---

## ☠️ Warning Signs You’re in a Retry Loop

- Same message keeps coming back to the DLQ
    
- DLQ topic size grows endlessly
    
- Processing logs repeat same message ID over and over
    

---

## ✅ Conclusion: DLQ is not a Retry Queue

🔹 DLQ is for **isolation**, **analysis**, and **manual inspection**,  
🔹 Not for infinite or automatic retrying — or you'll end up with **Kafka Groundhog Day**.

Let me know if you want a design template or Spring Kafka config for DLQ handling safely.

Hỏi ChatGPT
```


### Kafka vs RabbitMq

## 1. **Core Purpose**

- **RabbitMQ**:
    
    - Traditional **message broker**.
        
    - Focused on **message delivery guarantees**, routing, and flexible messaging patterns (point-to-point, pub-sub, request/reply, etc.).
        
    - Great for decoupling services and handling **task queues**.
        
- **Kafka**:
    
    - A **distributed event streaming platform**.
        
    - Built for **high-throughput, fault-tolerant, event-driven architectures**.
        
    - Excels at **real-time data pipelines**, event sourcing, and log aggregation.
        

---

## 2. **Architecture & Design**

- **RabbitMQ**
    
    - Broker-based, messages go into **queues**, consumers read and acknowledge them.
        
    - Supports **AMQP protocol** (and others like MQTT, STOMP).
        
    - Messages are usually **removed** once consumed.
        
    - Designed around **delivery guarantees** (at-most-once, at-least-once, exactly-once with effort).
        
- **Kafka**
    
    - Distributed, partitioned, replicated **commit log**.
        
    - Messages are **persisted** on disk and can be **re-read many times** by different consumers.
        
    - Works best with **ordered streams** and consumer groups.
        
    - Scales horizontally across brokers and partitions.
        

---

## 3. **Performance**

- **RabbitMQ**
    
    - Great for **low-latency, high-reliability message delivery**.
        
    - Not ideal for extremely high-throughput event streaming (millions/sec).
        
    - Better suited for workloads where **message state and routing logic** are important.
        
- **Kafka**
    
    - Designed for **high throughput and scalability** (millions of messages/sec).
        
    - Lower latency when processing large streams of data.
        
    - Works well for **big data pipelines** (integrates with Spark, Flink, Hadoop, etc.).
        

---

## 4. **Use Cases**

- **RabbitMQ** ✅
    
    - Background jobs / task queues
        
    - Request/response between services
        
    - Reliable communication in microservices
        
    - Complex routing (direct, fanout, topic exchanges)
        
- **Kafka** ✅
    
    - Event-driven architecture
        
    - Real-time analytics
        
    - Log aggregation / Change Data Capture (CDC)
        
    - Event sourcing and replay
        
    - Streaming data pipelines between systems
        

---

## 5. **Message Retention**

- **RabbitMQ**:
    
    - Message typically removed after being consumed.
        
    - Persistence is possible, but not designed for long-term storage.
        
- **Kafka**:
    
    - Messages stored for a **configurable retention period** (hours, days, or forever).
        
    - Consumers can **replay history**.
        

---

## 6. **Scalability**

- **RabbitMQ**:
    
    - Scaling can be done with clustering and sharding, but it’s not as seamless.
        
    - Better suited for **moderate workloads**.
        
- **Kafka**:
    
    - Extremely scalable due to partitioned log design.
        
    - Built for **distributed, fault-tolerant clusters**.
        

---

## 7. **When to Choose**

- Use **RabbitMQ** if you need:
    
    - Traditional messaging
        
    - Complex routing
        
    - Per-message acknowledgments
        
    - Small-to-medium workloads in microservices
        
- Use **Kafka** if you need:
    
    - Event streaming at scale
        
    - Replayability of events
        
    - High throughput & distributed processing
        
    - Integration with big data & stream processing


| Feature                 | **RabbitMQ** 🐇                                               | **Kafka** ⚡                                                     |
| ----------------------- | ------------------------------------------------------------- | --------------------------------------------------------------- |
| **Type**                | Message Broker                                                | Distributed Event Streaming Platform                            |
| **Architecture**        | Queue-based, broker manages delivery                          | Partitioned, replicated commit log                              |
| **Protocols**           | AMQP, MQTT, STOMP, etc.                                       | Custom TCP protocol                                             |
| **Message Handling**    | Consumed messages are usually removed from queue              | Messages are retained (for hours, days, or forever)             |
| **Throughput**          | Good for moderate workloads                                   | Extremely high (millions/sec)                                   |
| **Latency**             | Low latency per message                                       | Low latency, but optimized for throughput                       |
| **Ordering**            | Within a queue                                                | Within a partition                                              |
| **Scalability**         | Clustering & sharding, but limited                            | Horizontally scalable across partitions & brokers               |
| **Persistence**         | Messages can be persisted until consumed                      | Always persisted, replayable                                    |
| **Delivery Guarantees** | At-most-once, at-least-once, exactly-once (with effort)       | At-least-once (default), exactly-once (with configs)            |
| **Routing**             | Flexible routing (direct, topic, fanout exchanges)            | Simple: publish to topic, partition decides consumer            |
| **Best For**            | Task queues, request/response, microservices communication    | Event streaming, analytics, event sourcing, big data pipelines  |
| **Integrations**        | Many language clients, microservices-friendly                 | Strong ecosystem (Kafka Streams, Connect, Flink, Spark, Hadoop) |
| **Retention**           | Short-term (until ack/consume)                                | Configurable (hours → forever)                                  |
| **Analogy**             | Post office delivering letters (once delivered, they’re gone) | Newspaper publisher keeping archives (can re-read anytime)      |
### **Delivery Guarantees**

They define **how reliably a message is delivered from producer → broker → consumer**.

The three common levels are:

1. **At-most-once**
    
    - Message may be delivered **0 or 1 time**.
        
    - No retries, so it might be lost if a failure happens.
        
    - **Fastest but not reliable.**
        
2. **At-least-once**
    
    - Message is delivered **≥1 time**.
        
    - Retries ensure no message is lost.
        
    - But this can cause **duplicates**.
        
    - **Reliable but requires consumers to handle duplicates.**
        
3. **Exactly-once**
    
    - Message is delivered **only once** (no loss, no duplicates).
        
    - Hardest to achieve, requires coordination between producer, broker, and consumer.
        
    - More **latency/complexity**.


## 2. **RabbitMQ’s Guarantees**

- **Default**: **At-least-once** (messages stay in the queue until acknowledged).
    
- **At-most-once**: If consumer auto-acks without processing, messages can be lost.
    
- **Exactly-once**: Possible, but needs extra logic (idempotent consumers, transactions, or deduplication).
    

👉 RabbitMQ focuses on **reliability of message delivery** to consumers.

---

## 3. **Kafka’s Guarantees**

- **Default**: **At-least-once** (consumer commits offsets after processing).
    
- **At-most-once**: If consumer commits offset before processing → message may be lost.
    
- **Exactly-once**: Supported natively (since Kafka 0.11) with **idempotent producers + transactional APIs**.
    

👉 Kafka focuses on **durability + replayability**, and provides strong **exactly-once semantics** for streaming jobs.

---

## 4. **Example Scenarios**

- **At-most-once**: Logging user clicks (okay if you miss a few).
    
- **At-least-once**: Payment processing (better to retry than lose a transaction).
    
- **Exactly-once**: Bank transfers (must happen once and only once).
    

---

⚡ **In summary**:

- **RabbitMQ**: Naturally supports **at-least-once**, can do at-most-once and exactly-once with extra effort.
    
- **Kafka**: Naturally supports **at-least-once**, and has **built-in exactly-once** features for critical systems.


### Idempotent producer / consumer

An idempotent producer/consumer refers to a messaging or event processing pattern where the producer or consumer can safely send or process the same message multiple times without causing unintended side effects or inconsistencies in the system.

## Idempotent Consumer

An idempotent consumer ensures that processing the same message repeatedly results in the same outcome as processing it once. This is crucial in systems with "at-least-once" message delivery guarantees, where duplicate messages might be received. Implementing this pattern typically involves:

- Assigning a unique identifier to each message.
    
- Maintaining an idempotent repository (like a database table) of processed message IDs.
    
- Checking the repository before processing to discard duplicates.
    
- Updating the repository before or after processing to track processed messages safely.
    

This prevents issues like double processing, e.g., deducting the same amount multiple times from an account.[pradeepl+2](https://pradeepl.com/blog/patterns/idempotent-consumer-pattern/)

## Idempotent Producer

An idempotent producer guarantees that sending the same message multiple times (due to retries or failures) does not result in duplicate entries or actions in the consumer or messaging system. For example, in Kafka, idempotent producers ensure that retries during network glitches or acknowledgments don't create duplicate messages in the log, maintaining strict ordering and preventing duplicates.[oso+1](https://oso.sh/blog/how-to-build-truly-idempotent-kafka-consumers-a-mathematical-approach-to-handling-duplicates/)

## References
https://kafka.apache.org/documentation/
https://quarkus.io/guides/kafka#consumer-groups