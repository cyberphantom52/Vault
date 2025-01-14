A **socket** is an endpoint for sending and receiving data across a network. It acts as a bridge between the application layer and the transport layer in the OSI model, enabling communication between different processes, either on the same machine or over a network.

## Types

### By Communication Domain
#### AF_INET / AF_INET6
   - Used for communication over networks.
   
#### AF_UNIX (or AF_LOCAL)
   - Used for inter-process communication (IPC) on the same host.

#### AF_RAW
   - Provides access to lower-level protocols directly.
   - Used for network diagnostics, or implementing new protocols.

#### AF_PACKET
   - Used for low-level packet interfacing such as Network monitoring and packet capturing tools.
### By Socket Type
#### Stream sockets
- Known as `SOCK_STREAM`.
- Commonly uses [[TCP]].
- Connection oriented sockets where delivery of packets is guaranteed and data is delivered in-order.
#### Datagram sockets
- Known as `SOCK_DRAM`.
- Commonly uses [[UDP]]
- Connection-less protocol, delivery of packets is not guaranteed and data may be delivered out-of-order.
#### Raw sockets
- Known as `SOCK_RAW`. 
- Allows to send and receive IP packets without any specific protocol (TCP/UDP).
- Gives access to the protocol headers that are broadcast with the payload.
- Used for building transport-layer protocols that are not natively supported by the kernel.
## Working
### Components Involved
  A socket is uniquely identified by the combination of:
  - **IP Address:** Identifies a machine on the network.
  - **Port Number:** Identifies a specific application or service on that machine. (> 1024)
### Communication Process
  1. **Socket Creation:** An application creates a socket.
  2. **Binding:** The socket is bound to a specific IP address and port.
  3. **Listening/Connecting:** 
     - **Server:** Listens for incoming connections.
     - **Client:** Initiates a connection to the server.
  4. **Data Transfer:** Once connected, data can be sent and received.
  5. **Termination:** The connection is closed when communication ends.
