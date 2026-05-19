---
date: 2026-05-18
source: [[WA - 10]]
tags: [markup-languages, data-representation, web-standards]
---
# Markup Languages (SGML, HTML, XML, JSON)

## Overview
Analysis of the evolution and types of markup languages, from the general concept of "marking up" text to specialized standards for web presentation ([[HTML]]) and structured data interchange ([[XML]], [[JSON]]).

## Fundamentals of Markup
Markup is the act of adding annotations to a document to provide information about its structure or appearance. It is categorized into several types:
- **Punctuationally**: Provides syntactic information.
- **Presentational**: Deals with the layout and visual arrangement of content.
- **Procedural**: Consists of commands indicating how text should be formatted.
- **Descriptive**: Defines the type or class of the content.
- **Referential**: Refers to external entities, which are replaced during processing.
- **Meta-markup**: Provides means for controlling the interpretation of other markup and extending vocabularies.

## SGML (Standard Generalized Markup Language)
[[SGML]] is a descriptive and referential meta-markup language that serves as the foundation for other markup languages. It introduced the concept of the [[DTD]] (Document Type Definition) to define the structure of a document.

## HTML (HyperText Markup Language)
[[HTML]] is an application of SGML used to create hypertext web pages. It combines procedural, descriptive, and referential markup.
- **Issues**: Historically suffered from loose parsing, a lack of separation between content and presentation, and limited support for semantic descriptions.

## XML (Extensible Markup Language)
[[XML]] is a typed markup language designed for representing and exchanging semi-structured information, prioritizing interoperability among distributed systems.

### Structure and Validation
XML documents are represented as trees consisting of nodes: `TEXT`, `ELEMENT`, `ATTRIBUTE`, `COMMENT`, `PROCESSING INSTRUCTION`, and the `ROOT`.
The structure of an XML document can be defined and validated using:
- **[[DTD]]**: A legacy method with limitations regarding data types and namespaces.
- **[[XML Schema]]**: A more modern approach that uses XML syntax and supports complex data types.
- **[[XML Namespaces]]**: Used to avoid element name conflicts via the `xmlns` attribute.

### XML Processing APIs
Different APIs are used to parse and manipulate XML data:
- **[[Document Object Model]] (DOM)**: Creates an in-memory representation of the XML tree.
- **[[SAX]] (Simple API for XML)**: A push-based streaming API that notifies the application of events via callbacks.
- **[[StAX]] (Streaming API for XML)**: A pull-based streaming API that allows the application to request events.

## JSON (JavaScript Object Notation)
[[JSON]] is a lightweight data interchange format that is easier for humans to read and for machines to parse than XML.
- **Structures**: Based on two primary structures: **Objects** (name/value pairs) and **Arrays** (ordered lists).
- **Validation**: Uses **JSON Schema** for validation, documentation, and interaction control.
- **Parsing**: Often implemented using pull streaming APIs (e.g., the Jackson Project).
