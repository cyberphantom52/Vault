---
aliases:
  - RPC
  - IPC
---
- Function call within a process -> Local Call
![[Remote Procedure Call 2025-01-14 12.03.54.excalidraw|200|center]]
- RPC allows one machine to invoke a function on another machine as if it was a local function.
- Primary used as an [[Inter Process Communication]] mechanism when we want processes residing in different machines connected over the network to communicate.
- The process don't need to be aware of the network details.
- Uses [[Message Passing| Message Based Scheme]] for communication.
![[Remote Procedure Call 2025-01-14 12.16.37.excalidraw|1000|center]]


- Most popular implemetation of RPC is **gRPC**. It uses [[Protobuf|Protocol Buffer]] for underlying data transmission format.

## Basic Working
- RPC uses [[Message Passing]] for communications.
- RPC messages  well structured packets.
- Messages are sent to a RPC daemon listening on a port on the remote system.
- Each message contains an identifier of the function to execute and the parameters to be passed.
- The function is executed and output is returned back to the requested in a separate message.
### Client Side
- RPC provides a client side stub to abstract the communication details.
- A separate stub exists for each remote procedure.
- When a client invokes a remote procedure, RPC stub is invoked with the passed parameters.
- Stub locates the port on the server and packages/serializes the parameters in a format that can be transmitted over the network (See [[Protobuf|Protocol Buffer]]) and everything is passed as message to the server.
### Server Side
- A server side stub receives the message sent by the client and invokes the procedure.
- Any return values are passed back to the client using the same technique.


**Note:** In **gRPC**, client and server stubs are generated from `.proto` files, and parameters for remote procedure calls are marshalled(serialized) and unmarshalled(deserialized) using [[Protobuf|Protocol Buffer]] for efficient, **platform-independent** serialization, with the communication taking place over **[[HTTP Protocol Versions|HTTP/2]]** for enhanced performance and features like multiplexing, bidirectional streaming, and header compression.****

## Common Issues in RPC

| **Issue**                              | **Description**                                                                   | **Resolution**                                                                                   |
|----------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Difference in data representation between client and server** | Client and server may represent data differently (e.g., endianness, type mismatch). | Use common serialization formats like Protocol Buffers, Avro, or JSON to standardize data representation. |
| **Network errors leading to multiple or no execution** | Network issues can result in duplicate RPC calls or no execution of the request.   | Implement idempotent operations, retries with exponential backoff, and acknowledgments.          |
| **How does the client know the port number on the server** | The client may not know which port the server is listening on.                     | Use fixed RPC ports for well-known services or implement a matchmaking process for dynamic resolution. |
