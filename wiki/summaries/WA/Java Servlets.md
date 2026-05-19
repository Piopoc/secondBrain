---
date: 2026-05-18
source: [[WA - 05]]
tags: [java, servlets, web-architecture, jakarta-ee]
---
# Java Servlets and Web Container Architecture

## Overview
Analysis of the Java Servlet technology and the architectural role of the Web Container (Servlet Container) in the development of dynamic web applications.

## Web Server and Browser Interaction
The interaction between a client (Web Browser) and a Web Server is based on the HTTP request-response cycle.
- **Web Browser**: Consists of a Rendering Engine, a [[Document Object Model]] (DOM), a Scripting Engine (for event-driven logic), and a Parsing Engine.
- **Web Server**: Handles requests through Request Analysis and Access Control, using a Resource Handler to serve either **Static Resources** (files stored on server) or **Dynamic Resources** (generated on the fly).
- **AJAX**: Enables the modification of specific [[Document Object Model]] objects without reloading the entire page, a cornerstone of [[Web 2.0]].

## Java Servlets
A [[Java Servlet]] is a Java-based web component managed by a [[Web Container]] that generates dynamic content.

### The Web Container (Servlet Container)
The [[Web Container]] (e.g., [[Apache Tomcat]]) is crucial as it implements the [[Jakarta EE]] API and provides the execution environment for web components.
- **Packaging**: Applications are packaged into a standard **WAR (Web Application Archive)** file for distribution.
- **Control Inversion**: The container handles the entire lifecycle of the servlet object and its methods, rather than the servlet managing itself.

### Servlet Lifecycle
The container manages the servlet through four main stages:
1. **Instantiation**: The container creates an instance of the Servlet class.
2. **Initialization (`init()`)**: Called once after instantiation. Provides access to `ServletConfig` and `ServletContext`.
3. **Service (`service()`)**: Called for every request. It dispatches the request to specific methods based on the HTTP method (e.g., `doGet()`, `doPost()`).
4. **Destruction (`destroy()`)**: Called before the servlet is removed to clean up resources and synchronize state.

### Configuration and Mapping
The separation between Java code and the URL is achieved through the **Deployment Descriptor** (`web.xml`). This allows for high flexibility, as URLs can be changed without recompiling the logic.

## State Management and Concurrency
- **HTTP Statelessness**: HTTP is inherently stateless; each request is independent.
- **Stateful Applications**: To create useful web applications, state is managed using:
    - [[HttpSession]]: Identifies users and stores session-specific data.
    - **Cookies**: Small data fragments stored locally and sent to the server.
    - **Persistence**: Long-term state is kept in a database via the [[wiki/concepts/DAO Pattern]].
- **Concurrency**: Servlets are **multithreaded**. Each request runs on a different thread, meaning shared instance variables must be avoided to ensure thread-safety.

## Request Handling: GET vs POST
- **GET**: Sends parameters in the URL. Used for reading and searching data.
- **POST**: Sends parameters in the request body. Used for creating or modifying data.
- **Security**: Both methods send data in unencoded text and are therefore not secure without additional encryption (HTTPS).
