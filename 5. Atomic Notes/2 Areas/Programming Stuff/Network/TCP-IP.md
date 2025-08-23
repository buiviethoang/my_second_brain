2025-08-20 21:40
Status: #baby
Tags: [[network]]
## Main
TCP/IP (Transmission Control Protocol / Internet Protocol) is the fundamental communication model used for networks, including the internet. It defines **how data is packaged, addressed, transmitted, routed, and received** across networks.

### 🔹 Structure

TCP/IP is not a single protocol but a **suite of protocols**, organized in **layers**:

1. **Application Layer**
    
    - Provides services to the end user (e.g., web, email, file transfer).
        
    - Protocols: **HTTP/HTTPS, FTP, SMTP, DNS, DHCP**
        
2. **Transport Layer**
    
    - Ensures reliable or fast data delivery between applications.
        
    - Protocols:
        
        - **TCP (Transmission Control Protocol):** Reliable, connection-oriented, error-checked (used in web browsing, email).
            
        - **UDP (User Datagram Protocol):** Fast, connectionless, no guarantee of delivery (used in video streaming, gaming).
            
3. **Internet Layer**
    
    - Handles addressing, routing, and packet forwarding across networks.
        
    - Protocols: **IP (IPv4, IPv6), ICMP, ARP, RARP**
        
4. **Network Access (Link) Layer**
    
    - Deals with the physical transmission of data over network hardware.
        
    - Protocols: **Ethernet, Wi-Fi, PPP**

### With OSI [[OSI]]

|Feature|OSI Model (7 layers)|TCP/IP Model (4 layers)|
|---|---|---|
|Developed by|ISO (theoretical)|DARPA/DoD (practical)|
|Layers|7|4 (sometimes shown as 5)|
|Approach|General-purpose model|Internet-focused model|
|Transport|TCP, UDP|TCP, UDP|
|Network|IP, ICMP, OSPF|IP, ICMP, ARP|
|Usage|Conceptual reference|Real-world implementation|

### Mapping OSI → TCP/IP

- **Application, Presentation, Session → Application (TCP/IP)**
    
- **Transport → Transport (TCP/IP)**
    
- **Network → Internet (TCP/IP)**
    
- **Data Link + Physical → Network Access/Link (TCP/IP)**

## 📦 Analogy: Sending a Package

Imagine sending a parcel by courier:

- **Physical (wires/cables)** → The road the courier drives on.
    
- **Data Link (MAC, Ethernet)** → The courier’s license plate / ID card.
    
- **Network (IP)** → The address on the package.
    
- **Transport (TCP/UDP)** → Ensuring the package is delivered reliably (TCP) or just sent without guarantee (UDP).
    
- **Session** → Agreeing on when and how to communicate.
    
- **Presentation** → Packaging the gift (encryption, compression).
    
- **Application** → You writing the letter / ordering the product.

## References