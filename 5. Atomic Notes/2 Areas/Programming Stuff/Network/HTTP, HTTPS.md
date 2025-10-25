2025-08-20 21:50
Status: #baby
Tags: [[network]]
## Main
- **HTTP (HyperText Transfer Protocol):**  
    The protocol used by web browsers and servers to communicate (request/response model).
    
- **HTTPS (HTTP Secure):**  
    Same as HTTP but encrypted using **SSL/TLS**, ensuring confidentiality, integrity, and authentication.

## 🔹 Where They Fit in OSI & TCP/IP

### In the **OSI model**:

- **Application Layer**
    
    - HTTP/HTTPS run here.
        
    - Presentation Layer (encryption via SSL/TLS) may also be involved.
        
    - Session Layer helps manage the connection.
        

### In the **TCP/IP model**:

- **Application Layer**
    
    - HTTP/HTTPS protocols directly.
        
- **Transport Layer**
    
    - Uses **TCP** (not UDP) → ensures reliable, ordered delivery.
        
- **Internet Layer**
    
    - Uses **IP** to route data between client and server.
        
- **Link Layer**
    
    - Ethernet/Wi-Fi physically moves packets.

## 🔹 How an HTTP/HTTPS Request Works

Example: You visit **https://example.com** in a browser.

1. **DNS lookup** → resolve `example.com` to an IP.
    
2. **TCP handshake** → your computer and server establish a reliable connection.
    
3. **TLS handshake (only HTTPS)** → negotiate encryption keys & authenticate server.
    
4. **HTTP request** → Browser sends `GET /index.html HTTP/1.1`.
    
5. **Server response** → Sends back HTML, CSS, JS.
    
6. **Browser renders page** → Displays website to you.



| Feature      | HTTP                        | HTTPS                       |
| ------------ | --------------------------- | --------------------------- |
| Port         | 80                          | 443                         |
| Security     | Plain text (insecure)       | Encrypted via SSL/TLS       |
| Data Privacy | Anyone can sniff traffic    | Confidential & tamper-proof |
| Performance  | Slightly faster (no crypto) | A bit slower (handshake)    |
| Trust        | Not trusted by browsers     | Shows 🔒 lock icon          |

### HTTP versions

#### HTTP/1.0 (1996)

**Basic version**, defined in RFC 1945.

### 🔹 Key Characteristics:

- Each request opens a **new TCP connection** and closes it after the response.
    
- No **persistent connection** → very inefficient (slow if many requests).
    
- No **Host header** — meaning one server could only serve **one website per IP address**.

```pgsql
GET /index.html HTTP/1.0
User-Agent: Mozilla/5.0
```
#### HTTP/1.1 (1999)

**Major improvement** over 1.0, defined in RFC 2616 (and later RFC 7230–7235).

### 🔹 Key Improvements:

- ✅ **Persistent connections (Keep-Alive)** — reuse the same TCP connection for multiple requests/responses.
    
- ✅ **Pipelining** — send multiple requests before waiting for responses (though rarely used due to head-of-line blocking).
    
- ✅ **Host header required** — allows multiple domains on one IP (virtual hosting).
    
- ✅ **Chunked transfer encoding** — send data in chunks when size isn’t known in advance (like streaming).
    
- ✅ **Cache control** headers — better caching with `ETag`, `Cache-Control`, etc.

```
GET /index.html HTTP/1.1
Host: example.com
Connection: keep-alive
```
#### HTTP/2 (2015)

A **binary, multiplexed** protocol defined in RFC 7540 — designed to fix HTTP/1.1’s inefficiencies.

### 🔹 Key Improvements:

- ✅ **Binary framing** — data sent as binary frames (not plain text), faster to parse.
    
- ✅ **Multiplexing** — multiple requests/responses in parallel over one connection (no head-of-line blocking).
    
- ✅ **Header compression** using HPACK — reduces overhead.
    
- ✅ **Server push** — server can proactively send resources (e.g., CSS/JS) before the client asks.
    
- ✅ **Stream prioritization** — control which resources load first.

```
HEADERS (for GET /index.html)
DATA (HTML content)
HEADERS (for GET /style.css)
DATA (CSS content)
```

|Feature / Version|HTTP/1.0|HTTP/1.1|HTTP/2|
|---|---|---|---|
|Connection reuse|❌|✅|✅|
|Multiplexing|❌|⚠️ (pipelining, rarely used)|✅|
|Header compression|❌|❌|✅|
|Server push|❌|❌|✅|
|Binary framing|❌|❌|✅|
|Virtual hosting|❌|✅|✅|

### **API styles** and **HTTP protocol versions (1.0 / 1.1 / 2)**

## 🧩 1. **REST APIs**

✅ **Supported by:** HTTP/1.0, HTTP/1.1, HTTP/2

- REST is _built on top of HTTP_, so it directly uses the protocol (methods like `GET`, `POST`, etc.).
    
- Works perfectly over all versions — the protocol just affects performance, not API design.
    
- Most REST APIs today use **HTTP/1.1** or **HTTP/2** transparently through web servers or load balancers.

## 🧩 2. **GraphQL APIs**

✅ **Supported by:** HTTP/1.1, HTTP/2

- GraphQL usually runs **over HTTP** (typically `POST /graphql`), but it can also use **WebSockets** for subscriptions.
    
- Protocol version doesn’t matter much — the transport layer (HTTP/1.1 or HTTP/2) just improves performance.
    
## 🧩 3. **gRPC**

⚙️ **Requires:** HTTP/2 (mandatory)

- gRPC is built **specifically on top of HTTP/2** to leverage **binary framing**, **multiplexing**, and **header compression**.
    
- It will **not work** over HTTP/1.0 or HTTP/1.1.
    

> Example:
> 
> - Uses **binary protobuf messages**, not JSON.
>     
> - Communication looks like:
>

## 🧩 4. **SOAP**

✅ **Supported by:** HTTP/1.1 (and 1.0 technically)

- SOAP uses XML over HTTP (usually HTTP/1.1).
    
- It doesn’t need HTTP/2 but can work over it if the server supports it.

## 🧩 5. **WebSocket**

⚙️ **Starts over:** HTTP/1.1  
✅ **Can be used over:** HTTP/1.1 and HTTP/2

- WebSocket begins as an HTTP handshake (usually HTTP/1.1), then **upgrades** the connection to a bidirectional TCP stream.
    
- HTTP/2 supports it via **RFC 8441** (HTTP/2 WebSocket extension).

|API Style|HTTP/1.0|HTTP/1.1|HTTP/2|
|---|---|---|---|
|REST|✅|✅|✅|
|GraphQL|❌ (rare)|✅|✅|
|gRPC|❌|❌|✅ (required)|
|SOAP|✅|✅|⚙️ (optional)|
|WebSocket|❌|✅ (upgrade)|✅ (RFC 8441)|
## References