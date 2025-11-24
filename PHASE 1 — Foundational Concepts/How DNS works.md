Think of the **Domain Name System (DNS)** as the phonebook of the Internet.

Humans are good at remembering names (like `google.com`), but computers communicate using numbers (IP addresses like `142.250.190.46`). DNS translates the names we know into the numbers computers need.

Here is the step-by-step process of what happens between the moment you hit "Enter" and the moment the website loads.

---

### The Cast of Characters (The Servers)

Before the steps, you need to know who is doing the work. There are four main types of servers involved in a full lookup:

1. **Recursive Resolver ( The Librarian):** This is usually provided by your ISP (Internet Service Provider). It acts as your personal assistant, running around fetching information for you.
2. **Root Nameserver (The Index):** The first stop. It doesn't know the specific address, but it knows where to find the "top-level" information (like where all the `.com` or `.org` sites are listed).
3. **TLD Nameserver (The Section Manager):** This server manages the "Top-Level Domain" (TLD). If you want a `.com` site, this server knows exactly which Authoritative Server handles that specific website.
4. **Authoritative Nameserver (The Specific Book):** The final destination. This server contains the actual IP address you are looking for.

---

### The 8-Step Resolution Process

Imagine you type `www.example.com` into your browser.

### Phase 1: Checking Local Memory (Caching)

Before sending a request out to the internet, your computer checks if it has already done this work recently.

- **Step 1:** The **Browser** checks its own cache.
- **Step 2:** The **Operating System (OS)** checks its cache.
- **Step 3:** The **Router** checks its cache.
*(If the IP address is found in any of these, the site loads immediately. If not, we proceed to Step 4.)*

### Phase 2: The Query Journey

- **Step 4: The Ask:** Your computer asks the **Recursive Resolver** (ISP) for the IP address of `www.example.com`.
- **Step 5: The Root:** The Recursive Resolver doesn't know, so it asks the **Root Nameserver**. The Root Server replies, "I don't know `example.com`, but here is the address for the **.com TLD server**."
- **Step 6: The TLD:** The Resolver asks the **.com TLD Server**. This server replies, "I don't know the IP, but I know that **AWS Route53** (or GoDaddy, etc.) is the **Authoritative Nameserver** for `example.com`. Go ask them."
- **Step 7: The Authority:** The Resolver asks the **Authoritative Nameserver**. This server looks in its records and replies, "Yes, `www.example.com` is at IP address `93.184.216.34`."

[Image of DNS resolution process diagram](https://encrypted-tbn1.gstatic.com/licensed-image?q=tbn:ANd9GcSGAfMtm0lOBaRVoK_N_8GZ5p6PSQpGfnnNz7TJpORCMFnSF1vvyDUnTk9BgGkVcNeLibrJy4MU75yCbH-RgPjaVLiSeDM7nrIZ4btbI-BfsOV9PCY)

Shutterstock

### Phase 3: The Return

- **Step 8: Connection & Caching:** The Recursive Resolver sends the IP address back to your browser. Crucially, it also **saves (caches)** this number for a set amount of time (called TTL) so it doesn't have to repeat steps 5-7 next time you visit. Your browser now connects to the server and loads the webpage.

| **Server Type** | **Role in Analogy** | **Question it Answers** |
| --- | --- | --- |
| **Recursive Resolver** | Librarian / Assistant | "Let me go find that for you." |
| **Root Server** | Library Index | "I don't know, check the `.com` rack." |
| **TLD Server** | Rack Manager | "I don't know, check the `example.com` book." |
| **Authoritative Server** | The Book Page | "Here is the exact number you need." |