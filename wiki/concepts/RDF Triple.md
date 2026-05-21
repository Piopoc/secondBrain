# RDF Triple

An **RDF Triple** is the basic unit of information in the Resource Description Framework (RDF). It is a statement that asserts a relationship between two resources.

## Structure
A triple consists of three parts:
1. **Subject:** The entity that the statement is about (must be a URI).
2. **Predicate:** The property or relationship being asserted (must be a URI).
3. **Object:** The value or the entity that the subject is related to (can be a URI or a literal).

**Example:**
` <Bob> <knows> <Alice> `
- Subject: Bob
- Predicate: knows
- Object: Alice
