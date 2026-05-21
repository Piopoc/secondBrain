# JSON (JavaScript Object Notation)

**JSON** is a lightweight, text-based data-interchange format that is easy for humans to read and write and easy for machines to parse and generate.

## Role in Web Applications
JSON has become the de facto standard for data exchange between a client (browser) and a server, replacing XML in most modern APIs.

## Key Operations
- **Serialization:** Converting a JavaScript object into a JSON string using `JSON.stringify()`. This is used when sending data to a server.
- **Deserialization (Parsing):** Converting a JSON string back into a JavaScript object using `JSON.parse()`. This is used when receiving data from a server.

## Pros and Cons
- **Pros:** Concise, fast to parse, maps directly to JS objects.
- **Cons:** Strict syntax (one missing comma breaks the file), no native support for complex types like Dates or Functions.
