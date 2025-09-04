2024-12-07 21:48
Status: #baby
Tags: [[network]]
## Main
The **OSI model** is a **theoretical framework** for understanding and designing network systems. It has **7 layers**, each with its own role.

### 🔹 OSI Layers (Top → Bottom)

1. **Application Layer**
    
    - User-facing services: web browsing, email, file transfer.
        
    - Examples: HTTP, FTP, SMTP
        
2. **Presentation Layer**
    
    - Translates, encrypts, compresses data.
        
    - Examples: SSL/TLS, JPEG, MPEG
        
3. **Session Layer**
    
    - Establishes, manages, and terminates communication sessions.
        
    - Examples: NetBIOS, RPC
        
4. **Transport Layer**
    
    - Ensures reliable delivery, flow control, error handling.
        
    - Examples: TCP, UDP
        
5. **Network Layer**
    
    - Determines the best path, logical addressing.
        
    - Examples: IP, ICMP, OSPF
        
6. **Data Link Layer**
    
    - Node-to-node delivery, error detection, MAC addressing.
        
    - Examples: Ethernet, Wi-Fi, PPP
        
7. **Physical Layer**
    
    - Actual transmission of raw bits (cables, radio waves, hardware).


Open Systems Interconnection
7 layers
- Physical layer: bits -> devices (Hub / Modem / Repeater)
- Data link layer: Framing mess -> MAC, Flow control (Switches & Bridges)
- Network layer: Packet -> Ip address , Routing (Router & Switch)
- Transport layer: Segments -> TCP, UDP , Segmenting
- Session layer: Connections -> session establishment, sync
- Presentation layer: Formatted data -> JPEG, MPEG, TLS/SSL , Translation
- Application layer: Real data -> SMTP, FTP, DNS, ..

### Process
- ****Application Layer:**** Applications create the data.
- ****Presentation Layer:**** Data is formatted and encrypted.
- ****Session Layer:**** Connections are established and managed.
- ****Transport Layer:**** Data is broken into segments for reliable delivery.
- ***Network Layer:*** Segments are packaged into packets and routed.
- ****Data Link Layer:**** Packets are framed and sent to the next device.
- ****Physical Layer:**** Frames are converted into bits and transmitted physically.
## References
https://www.geeksforgeeks.org/open-systems-interconnection-model-osi/
