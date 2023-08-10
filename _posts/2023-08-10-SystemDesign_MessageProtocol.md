---
title: "[System Design] Message protocol"
categories:
  - System Design
tags:
  - System Design
---

# Connection-Oriented Request-Response with Notifications

> This is the messaging pattern traditionally used where connection-oriented messaging is used between the peers. The most common messaging procedure is Requst-Response (Req/Cfm/Rej) from client to server, but since the there is a connection, the server can also optionally send asynchronous notifications to the clients (Ind)​.

## Websocket / HTTP

> Once the connection is established, both the server and the client can send signals or messages to each other at any time, without a strict predefined order. This means that both sides have equal communication privileges, and they can initiate communication independently.

- **Connection Establishment**: The WebSocket connection is established through an initial HTTP-based handshake.

- **Bidirectional Communication**: Once the connection is established, both the client and the server can send messages or signals to each other independently and in real-time. There's no strict sequence or predefined initiator.

- **Simultaneous Interaction**: The client and server can exchange messages simultaneously, which is particularly useful for real-time updates, live data streams, and interactive applications.

- The WebSocket Protocol: The official specification for the WebSocket protocol by the Internet Engineering Task Force (IETF).

    - [RFC 6455: The WebSocket Protocol](https://tools.ietf.org/html/rfc6455)

- MDN Web Docs - WebSocket: The Mozilla Developer Network (MDN) provides detailed documentation and tutorials on using WebSocket in web development.

    - [MDN Web Docs: WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)

- WebSocket API Specification: The World Wide Web Consortium (W3C) provides an official specification for the WebSocket API, including methods, events, and examples.
    - [W3C WebSocket API Specification](https://www.w3.org/TR/websockets/)

- HTTP Ptotocol: [RFC 7231: Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://datatracker.ietf.org/doc/html/rfc7231)

- Encoding : [json](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
    - JSON (JavaScript Object Notation) is a lightweight data interchange format that is commonly used for encoding data in web applications, including WebSocket communication. JSON provides a way to represent structured data in a human-readable and easily parseable format. It is widely used for data serialization and communication between client and server.

- **Stateful** : The connection is maintained as long as both the client and the server keep it open. The state of the connection is maintained throughout the communication session. Both parties can send messages at any time, and the connection remains open until explicitly closed by either the client or the server. The server can keep track of the state of each connected client and maintain context between messages, allowing for more interactive and real-time applications.


## gRPC Streaming

# RESTful Request-Response

> This is the messaging pattern traditionally used in web services. The messaging procedure used is Request-Response from client to server. Clients always initiate with a request and procedure ends with a response from the server. ​

> There is a clear distinction between the client and the server roles, and there is a predefined sequence of interactions:

- **Client-Side Initiation** : The client initiates communication by sending an HTTP request to a specific resource on the server. The client specifies the HTTP method (such as GET, POST, PUT, DELETE) and the resource's URL.
- **Server-Side Response** : The server processes the client's request and sends back an HTTP response. The response typically contains the requested data or an acknowledgment, along with an appropriate status code.
- **Client Reception** : The client receives the server's HTTP response and acts based on the response data and status code.


> RESTful architecture emphasizes a few key principles, including:

- **Statelessness**: Each request from a client to a server must contain all the information necessary to understand and process the request. The server doesn't store client state between requests.
    - **REST(Representational State Transfer)** is an architectural style for designing networked applications, particularly web services, that relies on a **stateless** and client-server interaction model using HTTP.

- **Resource-Oriented**: Resources (e.g., URLs) are the main entities that clients interact with. Clients can use different HTTP methods to perform operations on these resources.

- **Uniform Interface**: The interactions between clients and servers are standardized, using a consistent set of HTTP methods (GET, POST, PUT, DELETE) and status codes (such as 200 OK, 404 Not Found).

- **Representation**: Data is exchanged between clients and servers in a standardized format, often using JSON or XML.

## gRPC

# Publish-subscribe

> In this messaging pattern Subscribers subscribe to Topics and Publishers publish messages on Topics. Usually there is a broker involved that broadcasts the message to all Subscribers that have subscribed to the Topic. In this way, Publishers are decoupled from Subscribers.​

## Redis​
> Redis acts as a broker so there are performance penalties compared to brokerless solutions, but it is a high performance, low footprint broker​

> In implementations with a broker there is an extra hop in the broker that can have an impact on performance for message intensive use cases. The extra hop will also impact latency that needs to be considered for use cases with requirements on latency. Redis feature key-space notification is an add-on to Redis Publish-Subscribe. With Key-space notifications the Subscribers subscribes to changes in the key-value database. When the Publisher updates the key-value database a notification is sent by Redis to the Subscribers that have subscribed to that Topic. Key-space notifications is an optional feature in Redis since enabling it have impact on performance. Redis Streams is an append-only data structure that models a log. Publishers append messages to the stream and Subscribers reads messages from the stream. As Redis streams models a log, Subscribers can read old entries from the stream in contrast to Redis Publish-Subscribes where the messages are sent in a fire-and-forget way. Redis Streams also have the Consumer Group concept that allows a group of clients to cooperate to consume a different portion of the same stream of messages.

- Publish-subscribe​
- Key-space notification​
- Streams​

# RPC

## Remote Procedure Call
> The opposite of a RESTful communication style is often referred to as "RPC" or "Remote Procedure Call" communication. RPC is a different approach to designing communication between distributed systems, and it contrasts with the principles of REST in several ways:

- **Stateful Communication**: Unlike REST, where each request is self-contained and stateless, **RPC communication often involves maintaining some form of state between calls.** This can lead to increased complexity and coupling between the client and server.

- **Method-Centric**: RPC focuses on invoking remote methods or procedures on the server. Clients send requests that specify the method to be executed along with the required parameters. This can lead to tight coupling between the client and server.

- **Complex Contracts**: RPC often relies on complex contracts or interfaces that define the methods, parameters, and return types that can be invoked remotely. Changes to these contracts can have a significant impact on both the client and server.

- **Less Emphasis on Resources**: REST places a strong emphasis on resources and their representations, making it a more natural fit for the web where resources can be easily identified by URLs. RPC tends to be more focused on actions or methods.

- **Uniform Interface**: RESTful communication follows a uniform interface, using standard HTTP methods (GET, POST, PUT, DELETE) and status codes. RPC may have a less standardized approach to method invocation and response handling.

- **Caching and Scalability**: REST promotes caching to improve performance, while RPC may have less emphasis on caching due to its stateful nature.

# GPB

> GPB stands for "Google Protocol Buffers," and it is a binary serialization format developed by Google. Protocol Buffers (protobuf) are designed to be a compact, efficient, and extensible way to serialize structured data for communication between systems. While JSON is a human-readable text-based format, GPB is a binary format that aims to be more efficient in terms of both size and parsing speed.

- **JSON**: JSON is a text-based format that represents data using human-readable strings, numbers, arrays, and objects, making it easy for humans to read and write. It's widely used for configuration files, APIs, and data interchange.
- **GPB**: Protocol Buffers use a binary format that is more compact and efficient for both data size and parsing speed. It's not human-readable, but it's optimized for efficient serialization and deserialization.