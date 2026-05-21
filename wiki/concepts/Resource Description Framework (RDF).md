# Resource Description Framework (RDF)

The **Resource Description Framework (RDF)** is the foundational data model for the Semantic Web. It provides a uniform way to express relationships between entities.

## The RDF Triple
The core of RDF is the **triple**, consisting of:
- **Subject:** The resource being described (URI).
- **Predicate:** The relationship or property (URI).
- **Object:** The value or related resource (URI or Literal).

A set of these triples forms an **RDF Graph**, where subjects and objects are nodes and predicates are directed arcs.

## RDF Syntaxes
RDF graphs can be encoded in various formats:
- **RDF/XML:** The original XML-based syntax.
- **N-Triples:** A simple, line-based plain text format.
- **Turtle:** A compact and human-readable text format.
- **JSON-LD:** A JSON-based syntax that integrates well with modern web APIs.
- **TriG:** An extension of Turtle that supports named graphs.
