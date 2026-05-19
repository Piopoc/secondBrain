---
date: 2026-05-18
source: [[WA - 07]]
tags: [java, jsp, mvc, architecture]
---
# JSP and MVC Architectural Pattern

## Overview
Analysis of the JavaServer Pages (JSP) technology and the implementation of the Model-View-Controller (MVC) architectural pattern in Java web applications.

## JavaServer Pages (JSP)
[[JavaServer Pages (JSP)]] is a technology that allows for the textual specification of dynamic web responses.

### JSP Lifecycle
The transformation from a JSP file to a running servlet follows a specific sequence:
1. **Translation**: The `.jsp` file is translated into a Java source file (`.java`) which is a [[Java Servlet]].
2. **Compilation**: The `.java` file is compiled into a bytecode class file (`.class`).
3. **Execution**: The web container loads the class and executes it. 
*Note: Translation and compilation occur only on the first invocation; subsequent requests use the compiled class directly for efficiency.*

### Components of JSP
- **Template Text**: Static HTML content.
- **[[JSP Directives]]**: Provide global information for the page.
- **[[JSP Actions]]**: Standard or custom operations performed by the server.
- **Scripting**: Raw Java code embedded in the page (generally avoided to maintain separation of concerns).
- **[[Expression Language (EL)]]**: A simplified language used to access data and variables made available by the application.
- **[[JSP Standard Tag Library (JSTL)]]**: A collection of standard tags (core, XML, formatting, database, functions) that reduce the need for scripting.

## Model-View-Controller (MVC) Paradigm
The [[MVC Architectural Pattern]] is used to decouple the application's internal representation of information from the ways that information is presented to and accepted from the user.

### The Three Components
1. **Model**: Represents the application state and business logic. Implemented using [[Java Beans]] and the [[wiki/concepts/DAO Pattern]].
2. **View**: Responsible for the presentation and visualization of output. Implemented using [[JavaServer Pages (JSP)]], HTML, CSS, and JavaScript.
3. **Controller**: Manages user input and coordinates the interaction between the Model and the View. Implemented using [[Java Servlet]]s.

### Interaction Flow
The typical request-response cycle in an MVC Java application is:
**User** $\rightarrow$ **Controller** (Servlet) $\rightarrow$ **Model** (Java Beans/DAO) $\rightarrow$ **Controller** $\rightarrow$ **View** (JSP) $\rightarrow$ **User**.

### Practical Application
- **Form Views**: JSP pages used for user input (e.g., `create-employee-form.jsp`).
- **Result Views**: JSP pages used to display the outcome of an operation (e.g., `create-employee-result.jsp`).
- **Controller Logic**: The servlet handles the request, invokes the necessary DAO to modify or retrieve data from the model, and forwards the result to the appropriate view.
