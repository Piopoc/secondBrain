---
date: 2026-05-18
source: [[WA - 08]]
tags: [web-services, rest, ajax, architecture]
---
# REST Web Services and AJAX

## Overview
Analysis of the **REST (Representational State Transfer)** architectural paradigm and its implementation in web services, coupled with the use of **AJAX** for asynchronous client-side communication.

## REST Architectural Paradigm
[[REST]] is an architectural style that applies the principles of the World Wide Web to the design of web services to achieve simplicity, statelessness, and scalability.

### Core Concepts
- **Resources**: Any entity with a unique and global identifier (URI). A resource has a **state** that can change over time.
- **Statelessness**: Each request from client to server must contain all the information necessary to understand the request. The server does not store any client context between requests.
- **Representations**: The server does not send the resource itself, but a **representation** of its state (e.g., [[JSON]], XML).

### Design Principles
To implement a RESTful service, the following steps are followed:
1. Identify the resources to be exposed.
2. Create descriptive URIs (using nouns).
3. Map HTTP methods to [[CRUD]] operations:
    - `GET` $\rightarrow$ Read
    - `POST` $\rightarrow$ Create
    - `PUT` $\rightarrow$ Update
    - `DELETE` $\rightarrow$ Delete
4. Use hypermedia (links) to allow navigation between resources.
5. Specify representation formats (schemas).
6. Document the services.

## Implementation in Java
The transition from a traditional [[DAO Pattern]] to a RESTful architecture involves moving from "data access" to "resource representation".

### Server-Side Architecture
- **Resource Interface**: Implementation using an `AbstractResource` class with a `toJSON` method for serialization.
- **JSON Handling**: Use of `JsonParser` and `JsonGenerator` for converting between Java objects and JSON strings.
- **RR Pattern**: A `RestResource` interface and an `AbstractRR` class (similar to the DAO pattern) that implement `serve` and `doServe` methods.
- **Routing**: The `web.xml` configuration maps the `/rest/*` URL pattern to a `RestDispatcherServlet`, which routes requests to the appropriate resource.

## AJAX (Asynchronous JavaScript and XML)
[[AJAX]] allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes.

### XMLHttpRequest Workflow
The standard process for making an asynchronous request is:
1. **Instantiation**: Create a new `XMLHttpRequest` object.
2. **Callback Definition**: Define the `onreadystatechange` function to handle the response once the server replies.
3. **Initialization**: Use `xhr.open(method, url, async)` to configure the request.
4. **Execution**: Use `xhr.send()` to transmit the request.

### Response Processing
The callback function must verify:
- **Ready State**: Ensure `xhr.readyState` is equal to `XMLHttpRequest.DONE`.
- **HTTP Status**: Check that `xhr.status` is `200` (OK) before processing the data.
