---
aliases:
  - Quick UDP Internet Connections
tags:
  - Internet
  - Networks
  - Networking
  - Network
  - TCP
  - UDP
  - HTTP
  - Protocol
---

- QUIC (Quick UDP Internet Connections) was Initially developed by Google.
- Standardized by the IETF in [RFC 9000](https://datatracker.ietf.org/doc/html/rfc9000).
- It's transport layer network protocol and works on top of [[UDP]]
- Designed to improve the performance of connection-oriented web applications.
- Addresses several limitations of traditional protocols like TCP, particularly in terms of latency, security, and reliability.
## Key Features

### Stream Multiplexing
- **Concurrent Streams:** Supports multiple independent streams within a single connection, enabling parallelism.
- **No HOL Blocking:** Issues in one stream do not block others, enhancing overall data throughput.

### Connection Establishment
- **0-RTT and 1-RTT Handshakes:**
  - **0-RTT:** Allows data to be sent without a full handshake if the client has previously communicated with the server.
  - **1-RTT:** Reduces the number of round trips required to establish a connection compared to TCP.
- **Faster Setup:** Overall connection establishment is quicker, reducing latency.

### Built-in Encryption
- **Integrated TLS 1.3:** QUIC incorporates encryption directly, ensuring all data is secure by default.

### Header Compression
- **Efficient Header Encoding:** Uses QPACK (similar to HTTP/2's HPACK) to compress HTTP headers, reducing overhead.
- **Improved Performance:** Minimizes the amount of data transmitted, speeding up request and response cycles.

### Forward Error Correction (FEC)
- **Error Recovery:** Implements mechanisms to recover lost packets without retransmission, improving reliability.
- **Reduced Latency:** Helps maintain data flow even in lossy network conditions.

### Improved Mobility Support
- **Connection Migration:** Supports seamless transition between different networks (e.g., switching from Wi-Fi to mobile data) without dropping connections.
- **Stable Connections:** Maintains session continuity, enhancing user experience on mobile devices.
## Differences Between QUIC and TCP

| Feature                   | QUIC                                | TCP                                  |
|---------------------------|-------------------------------------|--------------------------------------|
| **Underlying Protocol**  | UDP                                 | UDP                                  |
| **Connection Setup**     | 0-RTT/1-RTT handshakes              | 3-way handshake                      |
| **Multiplexing**         | Native support for multiple streams | Requires multiple connections or HTTP/2 |
| **Encryption**           | Integrated (TLS 1.3)                 | Optional (usually via TLS)           |
| **Head-of-Line Blocking**| Eliminated for streams              | Present at the transport layer       |
| **Congestion Control**   | Customizable within QUIC            | Standardized within TCP               |
| **Connection Migration** | Supported                            | Not inherently supported             |
| **Error Recovery**       | Built-in Forward Error Correction   | Relies on retransmission mechanisms  |
