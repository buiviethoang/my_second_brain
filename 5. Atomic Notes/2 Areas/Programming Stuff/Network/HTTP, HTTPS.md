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


## References