# **STATELESS vs STATEFUL SERVICES**

!https://media.geeksforgeeks.org/wp-content/uploads/20240515181222/Stateful-vs-Stateless-Architecture.webp

!https://media.geeksforgeeks.org/wp-content/uploads/20241009104650099648/Stateful-vs-Stateless-Microservices.webp

---

# 🧠 Why is this concept important?

Because **horizontal scaling ONLY works if your services are stateless**.

If your service is stateful → scaling becomes painful, complex, slow.

Let’s break it down very simple.

---

# 🚀 1. **STATELESS SERVICES**

A **stateless service does NOT store user/session data inside its memory**.

Every request is independent.

### ✔ No memory of previous request

### ✔ No user data stored inside application server

### ✔ Any server can handle any request

### **Example**

User sends request to `/login`

Server A handles it.

Next request `/home`

Server B can handle it.

Because the app doesn’t store state inside itself.

---

# 📦 Where is the state stored then?

In **external systems**:

- Database
- Redis
- Cache
- JWT Token
- Object Storage

NOT inside the application server.

---

# 🖼 Diagram (Stateless Scaling)

!https://substackcdn.com/image/fetch/%24s_%2138ak%21%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff968022c-7ceb-42e6-8aab-daa9e50edc59_1600x1029.png

https://www.researchgate.net/publication/321198405/figure/fig5/AS%3A740212003053571%401553491702406/Availability-and-reliability-through-redundant-stateless-microservices.ppm

```
Client
   |
   v
+-----------+
| Load Bal. |
+-----------+
   |    |    |
   v    v    v
 App1 App2 App3   <-- stateless
   \    |    /
    \   |   /
   +-----------+
   | Database |
   +-----------+

```

Since **App1, App2, App3** store NOTHING in memory →

LB can send user request to any server.

---

# 🎯 Benefits of Stateless Services

✔ **Best for horizontal scaling**

✔ Easy to add/remove servers

✔ High availability

✔ Each request is independent

✔ Crash-safe (no user data lost)

---

# 🛑 2. **STATEFUL SERVICES**

A stateful service **stores user/session data inside the server memory**.

This is dangerous for scaling.

### ❌ Keeps memory of user request

### ❌ Session stored on that server

### ❌ User must always be routed to same server

This is called **sticky sessions**.

---

# ⚠️ Example of Stateful

User logs in → Server A stores session in RAM.

Next request MUST go to Server A.

If Server A dies →

User gets logged out, service breaks → bad.

---

# ❌ Diagram (Stateful scaling is hard)

```
Client
   |
   v
+-----------+
| Load Bal. |
+-----------+
       |
   (Sticky routing)
       |
      App1  <-- stores session
     /    \
    DB    Redis

```

Only App1 can handle that user.

If App1 overloads → you cannot scale.

---

# 📌 Drawbacks of Stateful Services

✘ Bad for horizontal scaling

✘ Sticky sessions required

✘ More complex recovery

✘ Data loss if server crashes

✘ Hard to maintain and test

---

# 🏢 **Real-world Examples**

### **Stateless services (good design):**

- REST APIs
- Microservices
- Payment gateways
- Authentication with JWT
- Serverless (AWS Lambda, Cloudflare Workers)

### **Stateful services (harder to scale):**

- WebSockets (connections tied to server)
- Multiplayer game servers
- Video streaming sessions
- In-memory session-based apps

But even these are moving to stateless via:

- Redis session store
- Kafka
- Distributed cache
- Shared storage

---

# 🌟 How to Make SERVICES Stateless?

### ✔ 1. Don’t store session in server

Use:

- Redis
- Database
- JWT tokens

### ✔ 2. Don’t store uploaded files locally

Use:

- AWS S3
- Google Cloud Storage

### ✔ 3. Don’t store queues locally

Use:

- Kafka
- RabbitMQ

### ✔ 4. Don’t store long-lived connections on one machine

Use:

- WebSocket brokers
- Pub/Sub

---

# 🧩 Real Example for YOU (Instagram / WhatsApp style apps)

User sends request → LB → any service instance → service fetches from DB/Redis.