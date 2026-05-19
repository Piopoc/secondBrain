---
date: 2026-05-18
source: [[WA - 09]]
tags: [web-fundamentals, networking, http, uri]
---
# Web Communication Fundamentals

## Overview
Analysis of the basic technologies enabling web communication, focusing on resource identification ([[URI]]), data encoding and media types ([[MIME]]), the characteristics of the [[HTTP]] protocol, and basic authentication mechanisms.

## Resource Identification
The web relies on a standardized way to identify resources regardless of their nature (abstract or physical).

### The URI Hierarchy
A **[[URI]] (Uniform Resource Identifier)** is the most generic identifier. It embodies the information required to distinguish a resource.
- **[[URL]] (Uniform Resource Locator)**: A type of URI that provides the means of locating a resource by describing its primary access mechanism (e.g., network location).
- **[[URN]] (Uniform Resource Name)**: A type of URI that uniquely identifies a resource by name in a particular namespace (e.g., ISBN for books), independent of its location.
- **[[IRI]] (Internationalized Resource Identifier)**: An extension of URI that supports Unicode characters, allowing for a broader range of international scripts.

### URI Syntax
The general structure of a URI is:
`scheme:[//[user:password@]host[:port]][/path][?query][#fragment]`
- **Scheme**: Specifies the identifier (e.g., `http`, `ftp`, `telnet`).
- **Authority**: Includes optional authentication, the host (domain or IP), and an optional port.
- **Path**: Hierarchical data separated by slashes.
- **Query**: Attribute-value pairs used for parameters.
- **Fragment**: A pointer to a secondary resource within the main resource (e.g., a section heading).

## Data Encoding and Media Types
To ensure that different systems can interpret the data being exchanged, the web uses the [[MIME]] standard.

### MIME (Multipurpose Internet Mail Extensions)
[[MIME]] defines the nature of the data being sent.
- **Media Types**: Consist of a type (e.g., `text`, `image`, `audio`) and a subtype (e.g., `plain`, `html`, `xml`).
- **Content-Type Header**: The primary HTTP header used to communicate the MIME type.
- **Multipart Media Type**: Allows combining multiple data sets in one body using boundary delimiters. This is essential for web forms and file uploads via `multipart/form-data`.

### Java Implementation Details
In a Java enterprise environment:
- **File Uploads**: Handled as `byte[]` (byte arrays).
- **Configuration**: The `web.xml` file defines constraints for `multipart/form-data` uploads, such as maximum file size and the threshold for writing to disk.
- **Email Management**: Implemented via `jakarta.mail-api` and a `MailManager` class that reads SMTP configurations from a `.properties` file.

## HTTP Protocol Characteristics
The [[HTTP]] protocol defines how messages are formatted and transmitted.

### Properties of HTTP Methods
HTTP methods are categorized by their behavior:
- **Safe Methods**: Methods that do not modify the state of the resource (e.g., `GET`).
- **Idempotent Methods**: Methods that can be called multiple times without changing the result beyond the initial application (e.g., `PUT`, `DELETE`).
- **Cacheable Methods**: Methods whose responses can be cached by the client or intermediaries to improve performance.

## Authentication and Security
When a resource is protected, the server initiates an authentication challenge.
- **401 Status Code**: Returned by the server when authentication is required.
- **[[Basic Authentication]]**: The simplest form of authentication where the "username:password" string is encoded in **Base64**. It is explicitly noted as insecure because it lacks encryption.

## Infrastructure Integration
- **DB Pooling**: In Java web applications, database connection pooling is configured in `web.xml` using `javax.sql.DataSource` to optimize resource usage.
- **Session Management**: The controller must verify if the session is `NULL` to handle unauthenticated users.
