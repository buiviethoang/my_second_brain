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



### SSH? 
## 🔐 SSH (Secure Shell)

- A **network protocol** that allows **secure remote login and command execution** over an unsecured network.
    
- Commonly used by **system administrators and developers** to manage servers.
    
- Default port: **22**.

## 🔹 What SSH Does

1. **Secure Remote Access**
    
    - Lets you log in to another computer (server) and run commands securely.
        
2. **Encrypted Communication**
    
    - All traffic (commands, outputs, files) is encrypted — no eavesdropping possible.
        
3. **Authentication**
    
    - Supports password authentication or **public/private key pairs** (preferred, more secure).
        
4. **Tunneling & Port Forwarding**
    
    - Can forward ports (e.g., tunnel database traffic securely).
        
5. **File Transfers**
    
    - Protocols like **SCP** and **SFTP** run over SSH for secure file transfers.

|Feature|SSH (Secure Shell)|TLS/SSL (Transport Layer Security)|
|---|---|---|
|Purpose|Remote login, shell access, tunneling|Securing web traffic (HTTPS), emails, etc.|
|Typical Port|22|443 (HTTPS), 465/587 (SMTP), 993 (IMAP), etc.|
|Encryption|Symmetric + asymmetric (RSA, Ed25519, etc.)|Symmetric + asymmetric (RSA, ECDSA, etc.)|
|Authentication|Passwords, keys (public/private key)|X.509 certificates (CA signed)|
|Main Use Case|Administering servers, DevOps, tunneling|Secure browsing, online banking, APIs|

## 🔹 How SSH Works (simplified)

1. **Client initiates connection** → sends request to server on port 22.
    
2. **Key Exchange** → Client & server agree on an encryption method and exchange keys.
    
3. **Authentication** →
    
    - Password OR
        
    - Public key authentication (client proves it owns the private key).
        
4. **Secure Channel Established** → Now all commands & data are encrypted.


## 📦 Analogy

- **SSH** → Like having a **secure walkie-talkie** with the keys known only by you and the server, so you can send instructions safely.
    
- **TLS/SSL** → Like a **secure lock on a mailbox** where you exchange letters (web data).




## References