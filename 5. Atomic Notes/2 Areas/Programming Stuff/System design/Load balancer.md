2025-07-20 22:06
Status: #baby
Tags: [[system design]]
## Main

### What? 
Load balancers distribute incoming client requests to computing resources such as application servers and databases. In each case, the load balancer returns the response from the computing resource to the appropriate client. Load balancers are effective at:

- Preventing requests from going to unhealthy servers
- Preventing overloading resources
- Helping to eliminate a single point of failure

### 🔧 How it works:

When multiple clients send requests (e.g., to a website or API), the load balancer receives the requests first and decides **which server** (also called a **backend**, **node**, or **instance**) should handle each one.

### ⚙️ Types of Load Balancers:

#### 1. **Layer 4 Load Balancer (Transport layer)**

- Routes based on **IP address** and **TCP/UDP ports**.
- Example: Linux’s `iptables`, HAProxy in TCP mode.

#### 2. **Layer 7 Load Balancer (Application layer)**
- Routes based on **content** (like URL path, headers, cookies).
- More intelligent routing (e.g., `/api` requests go to service A, `/images` to service B).

### 📊 Common Load Balancing Algorithms:
- **Round Robin** – Rotate between servers in order. [[Round Robin]]
- **Least Connections** – Choose the server with the fewest active connections.
- **IP Hash** – Assign clients to servers based on their IP address.
- **Weighted Round Robin** – Give more requests to stronger servers.

### ✅ Benefits:
- Handles **traffic spikes** better.
- Prevents **downtime** by detecting and bypassing failed servers.
- Enables **horizontal scaling** (adding more servers instead of upgrading one big server). [[Horizontal scaling]]

### HAProxy
**HAProxy (High Availability Proxy)** is a **fast, reliable, and open-source** software used for **TCP** and **HTTP load balancing** and **proxying**.

It’s commonly used in **high-traffic websites** (like GitHub, Reddit, Twitter, Stack Overflow) due to its **efficiency, scalability**, and **fine-grained control**.

|Feature|Description|
|---|---|
|🔄 Load Balancing|Supports **round-robin**, **least connections**, **source-based hashing**, and more|
|📶 Protocol Support|Works at **Layer 4 (TCP)** and **Layer 7 (HTTP/HTTPS)**|
|❤️ Health Checks|Automatically disables backend servers if they are unhealthy|
|🔒 SSL/TLS Support|Termination and passthrough of HTTPS connections|
|🔍 Logging & Stats|Rich logs and a **web dashboard** for monitoring traffic and performance|
|🛡️ Security|Can rate-limit, filter requests, block IPs, and enforce ACL rules|

## 🧪 Common Use Cases

- Distribute traffic to multiple **web or API servers**
    
- Act as a **reverse proxy**
    
- Build a **high availability architecture**
    
- Terminate or forward **SSL connections**
    
- Protect upstream services using **ACLs** and **request filtering**
    

## 📑 Example Configuration

Here’s a minimal HAProxy config that load balances two web servers:

`global     log /dev/log local0     maxconn 2000     daemon  defaults     log     global     mode    http     timeout connect 5s     timeout client  50s     timeout server  50s  frontend http_front     bind *:80     default_backend web_servers  backend web_servers     balance roundrobin     server web1 192.168.1.101:80 check     server web2 192.168.1.102:80 check`

- **Frontend** receives incoming traffic on port 80.
    
- **Backend** load balances between `web1` and `web2`.
    

## 📊 Web Interface (Optional)

You can enable HAProxy’s stats page like this:

`listen stats     bind :8080     stats enable     stats uri /stats     stats refresh 10s`

Then access it at `http://yourserver:8080/stats`.

## 🚀 Why Use HAProxy?

- Extremely **lightweight and fast**
    
- Battle-tested in **production-grade systems**
    
- Handles **tens of thousands of concurrent connections**
    
- Highly configurable (ACLs, stickiness, headers, etc.)


## 🧰 How to Install (Linux)

`sudo apt update sudo apt install haproxy`

Then configure it in `/etc/haproxy/haproxy.cfg`.

### ACLs

In **HAProxy**, **ACLs (Access Control Lists)** are **rules** that help you **match conditions** in requests — like URLs, headers, IPs, or methods — and then take **specific actions** based on those conditions.

They let you do **conditional routing**, blocking, redirection, or logging.

## 🧠 Think of ACLs like this:

> “If the request matches this condition → do something.”
## ✅ Common Uses of ACLs in HAProxy

| Use Case                           | Example                                     |
| ---------------------------------- | ------------------------------------------- |
| Route based on URL path            | Send `/api/*` to a different backend        |
| Block an IP address                | Deny access from `192.168.1.100`            |
| Force HTTPS                        | Redirect all HTTP to HTTPS                  |
| Different routing based on headers | Route traffic based on user-agent or cookie |
| Limit access by method             | Allow only `GET`, deny `POST`               |

## 📑 Basic Syntax


`acl <name> <condition>`

`use_backend <backend_name> if <acl_name> http-request deny if <acl_name>`

## 🧪 Examples

### 1. **Route API traffic to a different backend**

`frontend http_front     bind *:80     acl is_api path_beg /api     use_backend api_backend if is_api     default_backend web_backend`

This checks if the path begins with `/api`, and if so, it sends the request to `api_backend`.

---

### 2. **Block specific IP address**

`frontend http_front     bind *:80     acl bad_ip src 192.168.1.100     http-request deny if bad_ip`

---

### 3. **Redirect HTTP to HTTPS**

`frontend http_front     bind *:80     acl is_http ssl_fc false     redirect scheme https if is_http`

---

### 4. **Allow only GET and HEAD methods**

`frontend http_front     bind *:80     acl invalid_method method POST PUT DELETE     http-request deny if invalid_method`

## 📚 Available Conditions (examples)

- `path`, `path_beg`, `path_end`, `hdr(host)`, `method`
    
- `src`, `dst` (source/destination IP)
    
- `ssl_fc` (if SSL is used)
    
- `req.body`, `req.len` (for request body or size)
    

## 🛡️ Tip

ACLs are **evaluated in order**, and multiple can be **combined** using `if` or `unless`.

`use_backend secure_api if is_api ssl_fc`


### Nginx

| Feature                          | **HAProxy**                                                | **Nginx**                                                                |
| -------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------ |
| 🔁 **Primary Purpose**           | Built for **high-performance load balancing**              | Built as a **web server** first, then added reverse proxy/load balancing |
| 🌐 **Layer Support**             | Strong at both **Layer 4 (TCP)** and **Layer 7 (HTTP)**    | Mostly **Layer 7 (HTTP)**, TCP/UDP support added later                   |
| ⚙️ **Performance**               | Extremely fast for high connection volume; low memory      | Very fast, but can fall behind HAProxy under very high connection churn  |
| 📊 **Monitoring / Stats**        | Detailed stats interface, granular metrics                 | Basic status module; more limited visibility                             |
| 🔀 **Load Balancing Algorithms** | Many options (round-robin, least-conns, source hash, etc.) | Fewer options (round-robin, least connections, IP hash)                  |
| 🔒 **SSL/TLS Support**           | Yes, full support                                          | Yes, often easier to configure                                           |
| 📁 **Static File Serving**       | ❌ No (not a web server)                                    | ✅ Yes (excellent at serving static files)                                |
| 🔧 **Configuration Complexity**  | More complex, especially ACLs                              | Simpler and more readable                                                |
| 💥 **Error Handling**            | Graceful error handling, retries, and timeouts             | Also solid, but fewer fine-tuned controls                                |
| 🧠 **Advanced Logic**            | Powerful **ACLs**, stick tables, connection tracking       | Simpler conditional logic with `if`, `map`, etc.                         |
| 📦 **Use Cases**                 | Load balancing, high availability                          | Web server + reverse proxy + static file server                          |


| Use This When...                                          | Use **HAProxy** | Use **Nginx**          |
| --------------------------------------------------------- | --------------- | ---------------------- |
| You need very **high-throughput** traffic routing         | ✅               | ❌                      |
| You’re serving **websites + APIs** from the same server   | ❌               | ✅                      |
| You want **powerful ACL-based routing**                   | ✅               | ⚠️ Limited             |
| You need **static file serving (images, HTML)**           | ❌               | ✅                      |
| You're managing **TCP/UDP services (e.g., MySQL, Redis)** | ✅               | ✅ (with stream module) |
| You want **easy config for HTTPS**                        | ⚠️              | ✅                      |

### Horizontal scaling vs load balancer

#### Without a load balancer:

`[Client] → [Single Server]`

- One server handles everything.
- If it goes down or becomes slow, the entire service suffers.

#### With a load balancer:

            +--> [Server 1]
[Client] -->|--> [Server 2]
            +--> [Server 3]
              (More servers can be added!)

- The **load balancer distributes requests** to available servers.
- You can add or remove servers **dynamically**.

✅ How Load Balancer Enables Horizontal Scaling

| Benefit                        | Explanation                                                   |
| ------------------------------ | ------------------------------------------------------------- |
| 🔀 **Traffic Distribution**    | Evenly spreads client requests across multiple servers        |
| 💥 **Failure Isolation**       | If one server fails, traffic is routed to others              |
| 🧱 **Add Capacity Seamlessly** | You can add new servers without changing how clients connect  |
| 🪄 **Elastic Scaling**         | In cloud environments, you can **auto-scale** based on demand |
| 🛡️ **Improved Availability**  | More servers = less downtime; load balancer monitors health   |
| 🚀 **No Single Bottleneck**    | Eliminates the issue of one server doing all the work         |

## 📦 Example in Action (Web App)

Let’s say your app has 3 servers:
`http://server1:3000 http://server2:3000 http://server3:3000`

You place an Nginx or HAProxy in front:

`http://loadbalancer:80`

The load balancer routes traffic to whichever server is available, healthy, and under the least load.

As traffic grows, you simply spin up **server4, server5, ...**, and the load balancer starts using them.

## 🧠 Bonus: In Cloud Environments

In AWS, GCP, Azure, etc., load balancers often work with **auto-scaling groups**:

- Monitor CPU/network load
    
- Automatically spin up/down instances
    
- Add new instances to the load balancer pool automatically
    
## 🔚 Conclusion

> A **load balancer makes horizontal scaling possible** by acting as a smart gatekeeper that distributes client requests to multiple backend servers. Without it, clients wouldn’t know how to reach those servers, or how to balance the load efficiently.

## References