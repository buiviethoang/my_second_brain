2025-08-20 21:53
Status: #baby
Tags: [[security]]
## Main
## 🔐 SSL (Secure Sockets Layer)

- **Older protocol** developed by Netscape in the 1990s.
    
- Versions: **SSL 2.0 (1995), SSL 3.0 (1996)**.
    
- Purpose: Encrypt communication between client (browser) and server.
    
- Problem: Now considered **obsolete and insecure** (vulnerable to many attacks).
    

---

## 🔐 TLS (Transport Layer Security)

- **Successor to SSL** — standardized by IETF.
    
- Versions: **TLS 1.0 (1999), TLS 1.1, TLS 1.2, TLS 1.3 (2018)**.
    
- Provides stronger encryption, more secure key exchange, better performance.
    
- TLS 1.2 and 1.3 are the **current secure standards**.

|Feature|SSL (old)|TLS (modern)|
|---|---|---|
|Status|Deprecated (insecure)|Actively used & secure|
|Latest Version|SSL 3.0 (1996)|TLS 1.3 (2018)|
|Handshake Security|Weak, vulnerable|Stronger, modern ciphers|
|Performance|Slower, more overhead|Faster, optimized|
|Browser Support|Removed from modern browsers|Fully supported everywhere|


## 🔹 TLS/SSL in HTTPS [[HTTP, HTTPS]]

- When you see **HTTPS://**, it really means **HTTP over TLS**.
    
- People still say _“SSL certificate”_, but technically, modern certificates are **TLS certificates**.


## 📦 Analogy

- **SSL** → like an **old padlock** that can be easily picked.
    
- **TLS** → like a **modern digital lock** with stronger keys and faster operation.
    

---

✅ **In short:**

- **SSL = Old, insecure**
    
- **TLS = New, secure standard (what HTTPS actually uses today)**





## References