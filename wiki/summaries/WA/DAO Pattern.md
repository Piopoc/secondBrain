---
date: 2026-05-18
source: [[WA - 06]]
tags: [java, architecture, dao, database]
---
# Java Enterprise Architecture and DAO Pattern

## Overview
Analysis of a full-stack Java application architecture, focusing on the [[Single Responsibility Principle (SRP)|separation of concerns]] through the 3-tier model, the implementation of the Data Access Object (DAO) pattern, and the optimization of database connectivity.

## Architectural Model
The application follows a **[[Three-tier Architecture]]**:
- **Presentation Logic (Client)**: User interface.
- **Application Logic (Server)**: Business rules and coordination, implemented via [[Java Servlet]]s.
- **Data Logic (Database)**: Persistent storage.

## Data Access Object (DAO) Pattern
The [[DAO Pattern]] is used to decouple the application logic from the underlying data source, ensuring that the business layer is agnostic of the database implementation. This embodies the [[Single Responsibility Principle (SRP)]] by giving each DAO class a single responsibility: data access.
- **Structure**: Each resource has a dedicated DAO that implements a common `DataAccessObject<T>` interface.
- **[[AbstractDAO]]**: A base class that provides uniform behavior for all DAOs, specifically managing connection opening and ensuring resources are released in `finally` blocks to prevent memory leaks.
- **Security**: DAOs must use `PreparedStatements` to prevent [[SQL Injection]] attacks.

## Resource Management
### Java Beans
[[Java Beans]] are used to model and transport data between tiers. To ensure thread safety in the multi-threaded environment of a servlet, these objects are designed to be **immutable** (using `final` and `private` fields, with no setter methods).

### Connection Pooling and JNDI
Establishing a database connection is a resource-intensive operation. To optimize performance:
- **Connection Pooling**: A pool of open connections is maintained by the [[Web Container]] (e.g., [[Apache Tomcat]]), eliminating the overhead of repeated authentication and socket opening.
- **[[JNDI]] (Java Naming and Directory Interface)**: Used to retrieve the connection pool configuration from the container. This avoids hardcoding sensitive credentials (IP, password, port) in the source code, improving security and portability.

## Implementation Details
- **`AbstractDBServlet`**: Centralizes the connection pool lifecycle, performing the JNDI lookup in `init()` and providing a `getConnection()` method for subclasses.
- **Configuration**: The connection pool is defined in `context.xml` and linked via `web.xml`.
- **Detailed Workflow**:
	1. **Client** sends HTTP request to web container
	2. **Web Container** routes request to appropriate **Servlet** (Controller)
	3. **Servlet** extracts request parameters and validates input
	4. **Servlet** invokes **DAO** method (Model) with parameters
	5. **DAO** obtains database connection from connection pool
	6. **DAO** prepares and executes SQL query using `PreparedStatement`
	7. **DAO** maps `ResultSet` to immutable **Java Beans**
	8. **DAO** returns Java Beans to **Servlet**
	9. **Servlet** sets Java Beans as request attributes
	10. **Servlet** forwards request to **JSP** (View) using `RequestDispatcher`
	11. **JSP** uses **EL and JSTL** to access data and generate HTML
	12. **Web Container** sends HTML response back to **Client**
