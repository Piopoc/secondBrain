# SPARQL

**SPARQL** (Simple Protocol and RDF Query Language) is the standard query language for RDF data. It allows users to retrieve and manipulate data stored in RDF format.

## Key Features
- **Pattern Matching:** Queries are based on "triple patterns" with variables (e.g., `?person foaf:name ?name`).
- **Query Forms:**
    - `SELECT`: Returns a table of results.
    - `CONSTRUCT`: Returns a new RDF graph.
    - `ASK`: Returns a boolean (true/false).
    - `DESCRIBE`: Returns a graph describing the resource.
- **Federated Queries:** Ability to execute queries across multiple distributed SPARQL endpoints.

## Result Formats
SPARQL supports multiple output formats to ensure interoperability: **XML, JSON, CSV, and TSV**.
