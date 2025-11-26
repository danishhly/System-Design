- Vertical vs Horizontal scaling
    
    # **SCALING TECHNIQUES — Vertical vs Horizontal Scaling**
    
    https://images.ctfassets.net/00voh0j35590/6wtOJjoIPbeqctg7dzjGS4/ca386d6416546a8ba6957e7b6407c5e4/vertical-versus-horizontal-scaling-compared-diagram.jfif
    
    !https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AwqWQdTXRwhmPG8leT7BeZA.png
    
    Scaling means:
    
    **How do we handle MORE users and MORE traffic without crashing?**
    
    There are two primary ways:
    
    ---
    
    # ✅ **1. Vertical Scaling (Scale Up)**
    
    ### **Meaning:**
    
    Increase power of the existing single machine.
    
    Think:
    
    👉 Add more **CPU**, **RAM**, **SSD**, **network** to ONE server.
    
    ### Example:
    
    - Your server has **2 CPU, 4GB RAM**
    - You upgrade it to **8 CPU, 32GB RAM**
    
    ### Simple diagram:
    
    ```
         BEFORE             AFTER
       +--------+         +----------+
       | 2 CPU  |   →     |  8 CPU   |
       | 4GB RAM|         | 32GB RAM |
       +--------+         +----------+
    
    ```
    
    ### **Pros**
    
    ✔ Simple — **no code changes**
    
    ✔ Quick — just upgrade the server
    
    ✔ Good for small systems
    
    ### **Cons**
    
    ✘ **Upper limit** — you can’t go beyond hardware limits
    
    ✘ Very expensive once you reach high-tier machines
    
    ✘ Single point of failure — if this machine dies, the system is down
    
    ### **Used When**
    
    - Early stage startup
    - Low traffic
    - Simple monolithic applications
    
    ---
    
    # ✅ **2. Horizontal Scaling (Scale Out)**
    
    ### **Meaning:**
    
    Add **more servers** and distribute load between them.
    
    Think:
    
    👉 Instead of 1 big machine, have **many small machines** working together.
    
    ### Example:
    
    1 server → 5 servers → 20 servers
    
    ### Diagram:
    
    !https://miro.medium.com/1%2AWVoaQNqS7rcR6gKUSNOvBQ.jpeg
    
    ```
                  +-------------------+
                  |  Load Balancer    |
                  +---------+---------+
                            |
       ----------------------------------------------
       |          |             |           |       |
    +------+   +------+     +------+    +------+ +------+
    | App1 |   | App2 |     | App3 |    | App4 | | App5 |
    +------+   +------+     +------+    +------+ +------+
    
    ```
    
    ### **Pros**
    
    ✔ Infinite scaling (just add more servers)
    
    ✔ Higher availability
    
    ✔ No single point of failure
    
    ✔ Cheaper overall
    
    ### **Cons**
    
    ✘ More complex
    
    ✘ Requires stateless services
    
    ✘ Needs load balancers, caching, distributed storage, etc.
    
    ### **Used When**
    
    - Large systems (Instagram, Netflix, Amazon)
    - Microservices
    - High traffic apps
    
    ---
    
    # ⚔️ **Vertical vs Horizontal Scaling — Quick Comparison**
    
    | Feature | Vertical Scaling | Horizontal Scaling |
    | --- | --- | --- |
    | **What grows?** | Power of **one** machine | Number of **many** machines |
    | **Complexity** | Simple | Complex |
    | **Limit** | Hard limit | Almost no limit |
    | **Failure** | Single point of failure | Highly available |
    | **Cost** | Expensive at high tiers | Cheaper distributed |
    | **Best for** | Small apps | Big apps / microservices |
    
    ---
    
    # 🧠 Practical Real-World Examples
    
    ### **Instagram / Facebook**
    
    - Uses **horizontal scaling**
    - Thousands of servers
    - Load balancers (L4 + L7)
    - Distributed cache (Redis)
    - Sharded databases
    
    ### **Small Startup Backend**
    
    - Uses **vertical scaling** at first
    - Later moves to horizontal scaling as users grow
    
    ---
    
    # 📝 When to Choose What?
    
    ### **Choose Vertical Scaling If:**
    
    - Your app is small
    - You’re in development
    - You don’t want to deal with distributed systems yet
    
    ### **Choose Horizontal Scaling If:**
    
    - You expect large traffic
    - You are using microservices
    - You want high availability
    - You need fault tolerance