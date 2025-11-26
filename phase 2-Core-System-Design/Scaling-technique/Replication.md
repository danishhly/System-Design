# **REPLICATION STRATEGIES in System Design**

!https://mariadb.com/sites/default/files/pictures/Images/dbreplication173.png

[https://educative.io/api/edpresso/shot/4882575048048640/image/5229808826187776.png](https://images.openai.com/static-rsc-1/xjlHCr9Leld8pM1qKPrwmgc7O10aFK-jo95kHW1pSWUHqtEKa2s85IiwBSqk_1Cc8Yn8lFevQO15ZTPTtAc8UputZpJzP_I9rGVF6LuvLmXwPjAa_vJ9HnLAVrYY0uQLD9r8JloT-3uUwnZGf0B3tA)

!https://user-images.githubusercontent.com/4745789/139211714-fc9266bd-ca22-48c4-9095-c6bff0ae99e6.png

**Replication = Keeping multiple copies of the same data on different servers.**

Why? → Performance, Fault tolerance, High availability.

There are **3 main replication strategies**:

1. **Leader–Follower (Master–Slave)**
2. **Master–Master (Multi-Leader)**
3. **P2P / Quorum / No-Single-Leader (Cassandra style)**

Let’s break them down.

---

# 1️⃣ **Leader–Follower Replication (MOST COMMON)**

Also called **Master–Slave**, **Primary–Replica**.

### 📌 How it works:

- **Leader handles all writes**
- **Followers replicate data from leader**
- Reads can be done from ANY follower

### 🔧 Example:

```
       Writes
        |
     +--------+
     | Leader |
     +--------+
      /   |   \
     /    |    \
+-------+ +-------+ +-------+
| F1    | | F2    | | F3    |
|Read   | |Read   | |Read   |
+-------+ +-------+ +-------+

```

### ✔ Pros

- Very simple
- Great read scalability
- Easy failover
- Popular in MySQL, PostgreSQL, MongoDB

### ❌ Cons

- Writes limited by one leader
- If leader dies → failover time
- Replication lag (small delay)

### ⭐ Best For

- 80% read, 20% write workloads
- Blogs, social media, dashboards

---

# 2️⃣ **Master–Master (Multi-Leader Replication)**

Two or more leaders accept writes.

!https://docs.oracle.com/cd/E19424-01/820-4806/images/repa.gif

### 📌 How it works:

```
 Client A → Leader 1
 Client B → Leader 2

 Leaders sync with each other

```

### ✔ Pros

- Higher write throughput
- No single write bottleneck
- Fast local writes (useful in multi-region)

### ❌ Cons

- **Conflict resolution required**
    
    (What if 2 clients write to same row at same time?)
    
- More complex setup
- More chances of inconsistency

### ⭐ Best For

- Multi-region apps
- Trading systems
- Collaborative applications (Google Docs-style)

### 🔥 Real-world examples

- MySQL Group Replication
- MongoDB Replica Sets (with multiple primaries allowed but rare)

---

# 3️⃣ **Peer-to-Peer / NoLeader / Quorum-Based Replication**

(Used by: **Cassandra, DynamoDB, ScyllaDB, Riak, CockroachDB**)

!https://www.scylladb.com/wp-content/uploads/apache-cassandra-architecture-diagram.png

!https://javawithloveblog.wordpress.com/wp-content/uploads/2019/12/image-2.png

### 📌 How it works:

- No fixed leader
- Every node can accept writes
- Reads/writes succeed only if enough nodes agree (**quorum**)

### Example:

```
Replication factor = 3
Quorum = 2

If 2 nodes respond → SUCCESS

```

### ✔ Pros

- Massive horizontal scaling
- No single point of failure
- Perfect for globally distributed systems
- Handles **huge write loads**

### ❌ Cons

- Complex design
- Eventually consistent (not immediate consistency)
- Harder to develop & reason about

### ⭐ Best For

- Instagram feed
- WhatsApp messages
- Amazon Dynamo-like workloads
- Time-series and big data

# 🔥 Real-World Use Cases

### **Leader–Follower**

- MySQL
- PostgreSQL
- Redis replication
- MongoDB (normal mode)

### **Multi-Leader**

- MySQL Multi-Primary
- MongoDB multi write regions
- Active-active databases

### **P2P / Quorum**

- Cassandra
- DynamoDB
- ScyllaDB
- CockroachDB

---

# 🧠 Interview-Ready Explanation (Use this!)

> “Replication is used for read-scaling, availability, and fault tolerance.
> 
> 
> The three common strategies are:
> 
> 1. Leader–Follower for simple consistent replication
> 2. Multi-Leader for multi-region write support
> 3. Leaderless/Quorum for massive scale and availability with eventual consistency.”
>

| Feature | Leader–Follower | Multi-Leader | P2P/Quorum |
| --- | --- | --- | --- |
| Write scalability | ⭐ Medium | ⭐⭐ High | ⭐⭐⭐ Huge |
| Read scalability | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ |
| Complexity | Low | Medium | High |
| Consistency | Stronger | Medium | Eventual |
| Failover | Manual/Auto | Auto | Built-in |
| Best use | Normal apps | Multi-region writes | Massive scale apps |