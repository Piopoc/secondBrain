---
date: 2026-05-18
source: [[WA - 02]]
tags: [web-evolution, architecture, distributed-systems]
---
# Web Evolution and Distributed Architectures

## Overview
Analysis of the evolution of the World Wide Web and the architectural patterns of distributed applications, from early conceptual precursors to modern n-tier systems.

## History and Evolution
The web evolved from conceptual machines for knowledge retrieval to a global decentralized infrastructure:
- **Precursors**: [[Vannevar Bush]]'s [[Memex]], [[Ted Nelson]]'s [[Project Xanadu]] (introducing [[HyperText]]), and [[Douglas Engelbart]]'s NLS system.
- **The Birth of WWW**: [[Tim Berners-Lee]] simplified these concepts into the [[World Wide Web]] using [[HTTP]], [[HTML]], and [[URL]].
- **Web Generations**:
    - [[Web 1.0]]: "Read Web" - static pages, passive consumption.
    - [[Web 2.0]]: "Read & Write Web" - dynamic participation, social media (AJAX, JSON, REST).
    - [[Web 3.0]]: "Semantic Web" - machine-readable data (RDF, OWL, SPARQL).
    - [[Web3]]: Decentralized systems with user-controlled data.
- **Hidden Web**:
    - [[Deep Web]]: Non-indexed content (dynamic URLs, databases).
    - [[Dark Web]]: Anonymous access via [[Tor]] or [[I2P]].

## Distributed Architectures
Modern web applications separate logic into three distinct layers: [[Presentation Logic]], [[Application Logic]], and [[Data Logic]].

### Architectural Patterns
1. **[[Single-tier Architecture]]**: All logic on one system (e.g., Mainframe). Simple but not scalable.
2. **[[Two-tier Architecture]]**:
    - **Fat Client**: Logic on client, data on server.
    - **Thin Client**: Logic on server, presentation on client.
3. **[[Three-tier Architecture]]**: Separation into Thin Client $\rightarrow$ Application Server $\rightarrow$ Database Server. High scalability and easy maintenance.

## Web Application Stack
Web applications are an implementation of the 3-tier model. They operate on a [[Web Application Stack]] (Request/Response) which sits atop the [[Network Stack]] (HTTP $\rightarrow$ TCP/UDP $\rightarrow$ IP $\rightarrow$ Physical).
