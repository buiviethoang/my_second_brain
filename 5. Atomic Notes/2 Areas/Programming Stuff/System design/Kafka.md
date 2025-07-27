2025-07-21 21:13
Status: #baby
Tags: [[computer science]] [[system design]]
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

|`acks` Value|Who Acknowledges|Performance|Durability|
|---|---|---|---|
|`0`|No one|🟢 Fastest|🔴 Risky|
|`1`|Leader only|🟡 Medium|🟡 Medium|
|`all` / `-1`|All replicas|🔴 Slowest|🟢 Strong|
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
## References
https://kafka.apache.org/documentation/
https://quarkus.io/guides/kafka#consumer-groups