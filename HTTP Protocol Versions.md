---
aliases:
  - HTTP
  - HTTPS
  - HTTP/1
  - HTTP/1.1
  - HTTP/2
  - HTTP/3
tags:
  - HTTP
  - Internet
  - Network
  - Networking
  - Networks
  - Protocol
  - TCP
  - UDP
---

## HTTP/1.0

Introduced in [RFC 1945](https://datatracker.ietf.org/doc/html/rfc1945).
### Key Features
- **Stateless:** Each request from client to server is independent.
- **Request-Response Model:** Clients send a request and wait for a response.
- **Separate TCP Connection:** Every HTTP request requires a new TCP connection.
### Problems with HTTP/1.0
1. **High Latency:**
   - Establishing a new TCP connection for every request introduces significant latency.
2. **Resource Intensive:**
   - Multiple connections lead to increased resource usage on both client and server.
3. **Limited Functionality:**
   - No support for persistent connections or pipelining.

## HTTP/1.1
- Introduced in [RFC 2068](https://datatracker.ietf.org/doc/html/rfc2068), later updated by [RFC 2616](https://datatracker.ietf.org/doc/html/rfc2616).

### Key Features
- **Persistent Connections:** Default use of keep-alive connections to reuse TCP connections.
- **Pipelining:** Multiple HTTP requests can be sent without waiting for corresponding responses.

### Problems with HTTP/1.1
1. **Head-of-Line (HOL) Blocking:**
   - With pipelining, a slow response can block subsequent requests.
2. **Limited Pipelining Support:**
   - Not widely supported by browsers due to complexity and reliability issues.
3. **Managing Multiple Connections:**
   - Browsers often open multiple TCP connections to bypass HOL blocking, leading to resource overhead.

## HTTP/2
- Introduced in [RFC 7540](https://datatracker.ietf.org/doc/html/rfc7540).
- It's a binary protocol where as versions 1 and 1.1 were text protocols.
### Key Features
- **Binary Framing Layer:** Encodes data into binary for more efficient parsing and transmission.
- **Multiplexing:** Multiple request-response streams concurrently over a single TCP connection.
- **Header Compression (HPACK):** Reduces the size of HTTP headers, improving performance.
- **Stream Prioritization:** Allows clients to indicate the priority of streams for better resource allocation.
- **Server Push:** Enables servers to send resources proactively without explicit client requests.

### Problems with HTTP/2
1. **TCP Limitations:**
   - Still subject to TCP's head-of-line blocking; a lost packet affects all streams.
2. **Complexity:**
   - More complex implementation compared to HTTP/1.x.
3. **TLS Requirement:**
   - Most browsers require HTTP/2 to operate over TLS, adding overhead.

## HTTP/3

- Introduced in [RFC 9114](https://datatracker.ietf.org/doc/html/rfc9114).
- Binary protocol based on **[[QUIC]]**

### Key Features
- **0-RTT Connection Setup:**
  - Reduces latency by allowing data transmission without a full handshake.
- **Multiplexed Streams Without HOL Blocking:**
  - Independent streams ensure that packet loss in one stream doesn't affect others.
- **Improved Security:**
  - Integrates TLS 1.3 directly into the protocol.
- **Better Mobile Performance:**
  - QUIC is designed to handle changing network conditions more gracefully.

### Advantages over HTTP/2
- **Elimination of TCP's Head-of-Line Blocking:** Each QUIC stream operates independently.
- **Faster Connection Establishment:** Reduced latency with 0-RTT and improved handshake processes.
- **Enhanced Compatibility with Modern Networks:** Better performance in environments with variable connectivity

## Summary

| Feature                   | HTTP/1.0                         | HTTP/1.1                | HTTP/2                           | HTTP/3                          |
| ------------------------- | -------------------------------- | ----------------------- | -------------------------------- | ------------------------------- |
| **Protocol Type**         | Text-based                       | Text-based              | Binary                           | Binary (QUIC-based)             |
| **Connection Handling**   | One request per TCP              | Persistent connections  | Multiplexing over one connection | Multiplexing via QUIC streams   |
| **Latency Issues**        | High due to multiple connections | Reduced with keep-alive | Improved with multiplexing       | Significantly reduced with QUIC |
| **Head-of-Line Blocking** | Yes                              | Yes                     | Yes                              | No                              |
| **Compression**           | None                             | Basic                   | Header compression (HPACK)       | Enhanced header compression     |
| **Security**              | Optional (HTTP)                  | Optional (HTTP)         | Typically over TLS               | Built-in TLS 1.3                |
| **Server Push**           | No                               | Limited                 | Yes                              | Yes                             |
