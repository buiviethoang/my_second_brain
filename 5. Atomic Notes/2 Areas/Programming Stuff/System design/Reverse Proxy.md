2025-07-24 22:22
Status: #baby
Tags: [[computer science]] [[system design]]
## Main
### What
A **reverse proxy** is a server that sits **between the client and one or more backend servers**. It receives requests from clients and **forwards them to the appropriate backend server**, then returns the response to the client.

It's the opposite of a forward proxy (which hides the client). A reverse proxy hides the backend.

🧠 Simple Analogy:
Imagine a receptionist at an office:

You (the visitor) talk only to the receptionist.

The receptionist speaks to the employee you want, then brings the answer back to you.
That receptionist is a reverse proxy.

Client (Browser)
    ↓
Reverse Proxy (e.g., Nginx, HAProxy)
    ↓
Backend Servers (App servers, APIs, etc.)


|Purpose|Benefit|
|---|---|
|🔒 **Security**|Hides internal servers from public access|
|🔁 **Load Balancing**|Distributes traffic among backend servers|
|🚪 **SSL Termination**|Handles HTTPS encryption so backends don’t have to|
|📉 **Caching**|Caches static or repeated responses to improve performance|
|🔃 **Compression**|Compresses responses before sending to client|
|📊 **Logging and Monitoring**|Centralizes logs for all backend traffic|
|🔀 **Routing**|Routes requests based on path, domain, headers, etc.|

## 💡 Examples of Reverse Proxy Software

- **Nginx** (most popular)
- **HAProxy**
- **Apache HTTPD (mod_proxy)**
- **Traefik**
- **Envoy**
- **AWS ALB / CloudFront / API Gateway** (cloud reverse proxies)


## 🧪 Real-World Example

### Without reverse proxy:

- Browser → `http://app1.mycompany.com`
    
- Browser → `http://app2.mycompany.com`
    

You must expose multiple ports/domains and handle everything separately.

### With reverse proxy:

- Browser → `http://www.mycompany.com`
    
- Reverse proxy routes:
    
    - `/api` → App server 1
        
    - `/auth` → App server 2
        
    - `/static` → CDN or cache
        

One public domain, centralized control.

| Proxy Type       | Hides        | Used by                                |
| ---------------- | ------------ | -------------------------------------- |
| 🔄 Reverse Proxy | **Backends** | Servers/Infra Teams                    |
| 🔼 Forward Proxy | **Clients**  | Users (for anonymity, filtering, etc.) |


|Feature|**Forward Proxy (aka Proxy)**|**Reverse Proxy**|
|---|---|---|
|🧍 Who it represents|**The client** (e.g., your computer)|**The server** (e.g., your web app)|
|🔒 Who it hides|Hides the **client** from the internet|Hides the **server** from the client|
|↔️ Traffic Direction|Client → Proxy → Internet|Client → Reverse Proxy → Backend Server|
|🧑‍💻 Common users|Users who want privacy, filtering, or control|Companies managing backend apps|
|🌐 Use cases|Bypass geo-blocks, ad filtering, school firewalls|Load balancing, SSL termination, routing|
|🧰 Examples|Squid, Shadowsocks, VPNs|Nginx, HAProxy, Traefik, Cloudflare|

## 🧠 Real-World Analogy

### Forward Proxy (Client-side):

> You (the client) want to access a website, but instead of going directly, you ask a middleman to fetch it for you.  
> The website never knows who you are — it only sees the middleman.

### Reverse Proxy (Server-side):

> A company has multiple employees (servers), but you always talk to the receptionist (the reverse proxy).  
> The receptionist decides which employee handles your request.
## References
https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/