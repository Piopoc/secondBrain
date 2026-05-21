# Semantic Web and Linked Data — Detailed Summary

> **Course:** Web Applications — Master Degree in Computer Engineering, Cybersecurity, and ICT for Internet and Multimedia
> **Academic Year:** 2025/2026
> **Author:** Nicola Ferro — University of Padua

---

## 1. Evolution of the Web

### 1.1 From Web of Documents to Web of Data

Initially, the Web was designed as a **hypertext** composed of resources — HTML documents, images, and other media — so that human beings could browse, surf, and access them. This original vision, often referred to as the "Web of Documents," was primarily oriented toward human consumption: pages were designed to be read by people, and the links between pages were meant to facilitate human navigation.

The current vision of **Web 3.0** encompasses a much broader range of resources, namely **data** — genoma and proteins, clinical trials, scientific and statistical data, Internet-of-Things streaming data — which need to be connected by means of **typed links** so that their structure and semantics are explicit and they can be accessed by **both human beings and machines**. This shift from a Web of Documents to a Web of Data represents a fundamental change in how information is structured, shared, and processed on the Internet.

The Web of Documents and the Web of Data are not mutually exclusive; rather, the Web of Data builds upon and extends the existing infrastructure of the Web of Documents. The key difference is that in the Web of Data, information is structured and linked in a way that machines can understand and process autonomously, enabling automated reasoning, data integration, and knowledge discovery at scale.

### 1.2 Data and Information

Raw data, by itself, has limited utility. A collection of numbers — such as 123, 91, 38.5, and 7 — carries no inherent meaning. It is only when these numbers are associated with labels or schemas that they become **information**. For example, associating 123 with "Heartbeat," 91 with "Pressure," 38.5 with "Temperature," and 7 with "Age" transforms raw data into meaningful information about a patient's vital signs.

Going further, by adding a schema that groups these attributes under a named entity (e.g., "Name: Luca, Age: 7, Temperature: 38.5, Heartbeat: 91, Pressure: 123"), we create a structured record that can be shared, queried, and integrated with other records. This process of adding structure and semantics to raw data is at the heart of the Semantic Web vision.

### 1.3 The Interoperability Challenge

A critical challenge in the Web of Data is making **different databases interoperate**. Various organizations and systems store data in different formats, using different schemas and different identifiers. Without a common framework for describing and linking data, these databases remain isolated "silos" of information. The Semantic Web addresses this challenge through the use of **ontologies** (which define shared conceptualizations) and **linked data** (which uses global identifiers and typed links to connect data across sources).

---

## 2. Semantic Representation of Knowledge

### 2.1 The Layers of Semantic Representation

The semantic representation of knowledge in the Web context involves three interconnected layers:

1. **Ontology (OWL — Web Ontology Language):** This layer defines the **concepts** — the abstract categories and relationships that exist in a domain. For example, the concept of "dog" as a species is defined at this level. OWL provides a rich, formal language for expressing ontologies with precise semantics, supporting advanced reasoning capabilities such as classification, consistency checking, and inference.

2. **Linked Data (RDF — Resource Description Framework):** This layer deals with **specific instances** — individual entities that belong to the concepts defined in the ontology. For example, "Linneo" is a specific dog (a particular instance of the concept "dog"). RDF provides the data model for describing these instances and their relationships using triples (subject-predicate-object).

3. **Knowledge Graph / Knowledge Base:** This is the collection of all the data (instances and their relationships) organized according to the ontology. It is the concrete, queryable representation of the knowledge in a domain. Knowledge graphs combine the schema-level definitions of the ontology with the instance-level data of linked data to create a rich, interconnected data structure.

The relationship between these layers is hierarchical: the ontology provides the conceptual framework, linked data populates this framework with specific instances, and the knowledge graph is the resulting integrated data resource that can be queried and reasoned over.

---

## 3. Resource Description Framework (RDF)

### 3.1 Introduction to RDF

RDF is a framework for representing information on the Web. It is the foundational data model of the Semantic Web, providing a uniform way to express relationships between entities using a simple yet powerful structure.

The core structure of the RDF data model is a set of **RDF triples**, each consisting of three components:

- **Subject** (a URI): The resource being described.
- **Predicate** (a URI): The relationship or property being asserted.
- **Object** (a URI or a literal): The value or resource that the subject is related to.

Asserting an RDF triple means stating that some relationship, indicated by the predicate, holds between the resources denoted by the subject and object. The statement corresponding to an RDF triple is known as an **RDF statement**.

A set of such triples is called an **RDF graph**. An RDF graph can be visualized as a node-and-directed-arc diagram, in which each triple is represented as a node-arc-node link: the subject and object are nodes, and the predicate is a directed arc from the subject to the object.

An **RDF document** is a document that encodes an RDF graph in a concrete RDF syntax. There are several syntaxes available, including:

- **RDF/XML**: An XML-based syntax (the original RDF syntax).
- **N-Triples**: A simple line-based, plain-text format.
- **Turtle**: A more compact and readable plain-text format.
- **JSON-LD**: A JSON-based syntax that integrates well with existing web technologies.
- **RDFa**: For embedding RDF in HTML and XML.
- **TriG**: An extension of Turtle that supports named graphs.

### 3.2 Example of RDF

The course material uses a running example involving a person named Bob, who knows Alice, has an interest in the Mona Lisa, and was born on July 4, 1990. The Mona Lisa is further described with its title and its creator (Leonardo da Vinci), and a Europeana item is linked as a subject of the Mona Lisa. This example illustrates how RDF triples can represent a rich network of relationships between entities from different sources (FOAF vocabulary for social relationships, Schema.org for birth dates, Dublin Core for titles and creators, and Wikidata for entity identifiers).

### 3.3 RDF/XML Syntax

RDF/XML was the original syntax for RDF, developed in the late 1990s. It provides an XML-based encoding of RDF graphs. The following example encodes the Bob/Mona Lisa graph:

```xml
<?xml version="1.0" encoding="utf-8"?>
<rdf:RDF
  xmlns:dcterms="http://purl.org/dc/terms/"
  xmlns:foaf="http://xmlns.com/foaf/0.1/"
  xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
  xmlns:schema="http://schema.org/">
  <rdf:Description rdf:about="http://example.org/bob#me">
    <rdf:type rdf:resource="http://xmlns.com/foaf/0.1/Person"/>
    <schema:birthDate rdf:datatype="http://www.w3.org/2001/XMLSchema#date">1990-07-04</schema:birthDate>
    <foaf:knows rdf:resource="http://example.org/alice#me"/>
    <foaf:topic_interest rdf:resource="http://www.wikidata.org/entity/Q12418"/>
  </rdf:Description>
  <rdf:Description rdf:about="http://www.wikidata.org/entity/Q12418">
    <dcterms:title>Mona Lisa</dcterms:title>
    <dcterms:creator rdf:resource="http://dbpedia.org/resource/Leonardo_da_Vinci"/>
  </rdf:Description>
  <rdf:Description rdf:about="http://data.europeana.eu/item/04802/243FA8618938F4117025F17A8B813C5F9AA4D619">
    <dcterms:subject rdf:resource="http://www.wikidata.org/entity/Q12418"/>
  </rdf:Description>
</rdf:RDF>
```

In RDF/XML, triples are specified within an `rdf:RDF` element. The attributes of the `rdf:RDF` start tag provide namespace prefixes for writing element names concisely. Each `rdf:Description` element describes a subject, and its child elements represent the predicates and objects of triples about that subject. When the object is an IRI, it is specified via the `rdf:resource` attribute; when the object is a literal, its value is entered as the content of the property element, with optional datatype specification.

### 3.4 N-Triples Syntax

N-Triples provides a simple, line-based, plain-text way of serializing RDF graphs. Each line represents a single triple. Full IRIs are enclosed in angle brackets (`<>`), and a period at the end of each line signals the end of the triple. The following example encodes the same graph:

```n-triples
<http://example.org/bob#me> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://xmlns.com/foaf/0.1/Person> .
<http://example.org/bob#me> <http://xmlns.com/foaf/0.1/knows> <http://example.org/alice#me> .
<http://example.org/bob#me> <http://schema.org/birthDate> "1990-07-04"^^<http://www.w3.org/2001/XMLSchema#date> .
<http://example.org/bob#me> <http://xmlns.com/foaf/0.1/topic_interest> <http://www.wikidata.org/entity/Q12418> .
<http://www.wikidata.org/entity/Q12418> <http://purl.org/dc/terms/title> "Mona Lisa" .
<http://www.wikidata.org/entity/Q12418> <http://purl.org/dc/terms/creator> <http://dbpedia.org/resource/Leonardo_da_Vinci> .
<http://data.europeana.eu/item/04802/243FA8618938F4117025F17A8B813C5F9AA4D619> <http://purl.org/dc/terms/subject> <http://www.wikidata.org/entity/Q12418> .
```

Line 3 shows an example of a typed literal (a date). String literals are so ubiquitous that N-Triples allows omitting the datatype — `"Mona Lisa"` is equivalent to `"Mona Lisa"^^xsd:string`. For language-tagged strings, the datatype is `rdf:langString` and is never specified explicitly.

### 3.5 JSON-LD Syntax

JSON-LD provides a JSON syntax for RDF graphs and datasets. It can transform existing JSON documents into RDF with minimal changes and offers universal identifiers for JSON. The following example encodes the same graph:

```json
{
  "@context": "example-context.json",
  "@id": "http://example.org/bob#me",
  "@type": "Person",
  "birthdate": "1990-07-04",
  "knows": "http://example.org/alice#me",
  "interest": {
    "@id": "http://www.wikidata.org/entity/Q12418",
    "title": "Mona Lisa",
    "subject_of": "http://data.europeana.eu/item/04802/243FA8618938F4117025F17A8B813C5F9AA4D619",
    "creator": "http://dbpedia.org/resource/Leonardo_da_Vinci"
  }
}
```

The `@context` key points to a JSON document that describes how the document can be mapped to an RDF graph. Each JSON object corresponds to an RDF resource. The `@type` key specifies the type of the resource, and other keys map to RDF properties. Nested JSON objects represent related resources.

The corresponding JSON-LD context specification maps short property names to full RDF IRIs:

```json
{
  "@context": {
    "foaf": "http://xmlns.com/foaf/0.1/",
    "Person": "foaf:Person",
    "interest": "foaf:topic_interest",
    "knows": {
      "@id": "foaf:knows",
      "@type": "@id"
    },
    "birthdate": {
      "@id": "http://schema.org/birthDate",
      "@type": "http://www.w3.org/2001/XMLSchema#date"
    },
    "dcterms": "http://purl.org/dc/terms/",
    "title": "dcterms:title",
    "creator": {
      "@id": "dcterms:creator",
      "@type": "@id"
    },
    "subject_of": {
      "@reverse": "dcterms:subject",
      "@type": "@id"
    }
  }
}
```

The context maps terms like "Person", "interest", and "knows" to types and properties in the FOAF and Schema.org vocabularies, while also specifying datatypes and whether values should be interpreted as IRIs.

### 3.6 TriG Syntax (Multi-Graph)

TriG is an extension of the Turtle syntax that supports **named graphs**. This allows an RDF dataset to contain multiple graphs, each with its own name. The following example shows a multi-graph version of the running example:

```trig
BASE <http://example.org/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX schema: <http://schema.org/>
PREFIX dcterms: <http://purl.org/dc/terms/>
PREFIX wd: <http://www.wikidata.org/entity/>

GRAPH <http://example.org/bob> {
  <bob#me>
    a foaf:Person ;
    foaf:knows <alice#me> ;
    schema:birthDate "1990-07-04"^^xsd:date ;
    foaf:topic_interest wd:Q12418 .
}

GRAPH <https://www.wikidata.org/wiki/Special:EntityData/Q12418> {
  wd:Q12418
    dcterms:title "Mona Lisa" ;
    dcterms:creator <http://dbpedia.org/resource/Leonardo_da_Vinci> .
}

<http://data.europeana.eu/item/04802/243FA8618938F4117025F17A8B813C5F9AA4D619>
  dcterms:subject wd:Q12418 .

<http://example.org/bob>
  dcterms:publisher <http://example.org> ;
  dcterms:rights <http://creativecommons.org/licenses/by/3.0/> .
```

This dataset contains two named graphs (identified by their URIs). The triples within each named graph are enclosed in curly braces. Triples that are not part of any named graph form the unnamed ("default") graph of the RDF dataset.

---

## 4. Semantics of RDF Graphs

### 4.1 Declarative Semantics

A key goal in the use of RDF is to be able to automatically **merge** useful information from multiple sources to form a larger collection that is still coherent and useful. The semantics of RDF are defined with mathematical precision in the RDF Semantics specification, but intuitively:

1. **IRIs are global:** The IRIs used to name the subject, predicate, and object are "global" in scope — they name the same thing each time they are used, regardless of which document or source they appear in. This global scope is what enables data from different sources to be merged unambiguously.

2. **Triples are truth-assertions:** Each triple is "true" exactly when the predicate relation actually exists between the subject and the object. Asserting a triple is making a claim about the world.

3. **Graphs are conjunctions:** An RDF graph is "true" exactly when all the triples in it are "true." A graph is the logical conjunction of its constituent triples.

### 4.2 Logical Inference and Entailment

One of the benefits of RDF having these declarative semantics is that systems can make **logical inferences**. That is, given a certain set of input triples which they accept as true, systems can in some circumstances derive additional true statements that were not explicitly stated.

Given the flexibility of RDF, where new vocabularies can be created whenever people want to use new concepts, there are many different kinds of reasoning one might want to perform. When a specific kind of reasoning is needed, it is defined as an **entailment regime**. Some entailment regimes are fairly easy to implement and reasoning can be done quickly, while others require sophisticated techniques to implement efficiently.

For example, consider the following two statements:

```turtle
ex:bob foaf:knows ex:alice .
foaf:knows rdfs:domain foaf:Person .
```

From these two statements, a system can infer that `ex:bob` is a `foaf:Person`, even though this was never explicitly stated. This inference is made possible by the RDFS (RDF Schema) entailment regime, which defines the semantics of the `rdfs:domain` property.

---

## 5. SPARQL — Simple Protocol and RDF Query Language

### 5.1 Introduction to SPARQL

**SPARQL** (Simple Protocol and RDF Query Language) is a set of specifications that provide languages and protocols to query and manipulate RDF graph content on the Web or in an RDF store. SPARQL 1.1 is the current version, standardized as a W3C Recommendation in March 2013.

The SPARQL 1.1 family of specifications includes:

- **SPARQL 1.1 Query Language:** A query language for RDF that supports pattern matching, filtering, optional parts, unions, and construction of new RDF graphs from query results.
- **SPARQL 1.1 Update Language:** An update language for modifying RDF graphs (inserting, deleting, and loading data).
- **SPARQL 1.1 Protocol for RDF:** A protocol for conveying SPARQL queries and update requests to a SPARQL service over HTTP.
- **SPARQL 1.1 Graph Store HTTP Protocol:** A minimal means for managing RDF graph content via HTTP operations (REST-style).
- **SPARQL 1.1 Federated Query:** An extension for executing queries distributed over different SPARQL endpoints.
- **SPARQL 1.1 Entailment Regimes:** Defining the semantics of SPARQL queries under entailment regimes such as RDF Schema, OWL, or RIF.
- **SPARQL 1.1 Service Description:** A method for discovering and a vocabulary for describing SPARQL services.
- **SPARQL 1.1 Query Results Formats:** Specifications for returning query results in XML, JSON, CSV, and TSV formats.
- **SPARQL 1.1 Test Cases:** A suite of tests for understanding the specification and assessing conformance.

### 5.2 SPARQL Query Language Example

The course material provides an example using an RDF graph about Alice and her social contacts. The graph, published at `http://example.org/alice`, contains information about Alice, Bob, Charlie, and Snoop Dogg, along with their names, email addresses, and social connections (who knows whom).

Given this data loaded into a SPARQL service (an HTTP endpoint that processes SPARQL queries), a typical SPARQL query might look like:

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT ?name ?count
WHERE {
  ?person foaf:name ?name .
  ?person foaf:knows ?friend .
}
ORDER BY ?name
```

This query selects the names of people and their friends from the graph. The `WHERE` clause uses triple patterns with variables (`?person`, `?name`, `?friend`) that match against the triples in the RDF graph. The `SELECT` clause specifies which variable bindings should be returned. The `ORDER BY` clause sorts the results alphabetically by name.

SPARQL supports several query forms:
- **SELECT:** Returns variable bindings as a table of results.
- **CONSTRUCT:** Returns an RDF graph constructed from the query results.
- **ASK:** Returns a boolean indicating whether the query pattern matches.
- **DESCRIBE:** Returns an RDF graph describing the matched resources.

Complex queries may include **union** (combining results from alternative patterns), **optional** query parts (returning results even when some patterns don't match), and **filters** (applying constraints to variable bindings).

### 5.3 SPARQL Query Result Formats

SPARQL supports multiple result formats for exchanging query results in machine-readable form:

- **XML:** A structured XML format using `<sparql>`, `<head>`, and `<results>` elements, with `<result>` elements containing `<binding>` elements for each variable.

- **JSON:** A JSON format with `head`, `results`, and `bindings` keys. Each binding maps variable names to typed values with `type`, `value`, and optional `datatype` fields.

- **CSV/TSV:** Simple tabular formats suitable for processing with spreadsheet tools or data analysis pipelines.

The availability of multiple result formats makes SPARQL results accessible to a wide range of client applications, from web-based JavaScript applications (using JSON) to data analysis tools (using CSV).

---

## 6. Linked (Open) Data

### 6.1 Introduction to Linked Data

**Linked Data** is about using the Web to connect related data that was not previously linked, or using the Web to lower the barriers to linking data currently linked using other methods. The basic idea is to apply the general architecture of the World Wide Web to the task of sharing structured data on a global scale.

The term **Linked Data** refers to a set of best practices for publishing and interlinking structured data on the Web. When this data is explicitly published under an **open license**, it is called **Linked Open Data (LOD)**. The distinction is important: Linked Data is about the technical practices of connecting structured data, while Linked Open Data adds the legal dimension of open licensing, ensuring that the data can be freely used, reused, and redistributed.

### 6.2 Linked Data Principles

Tim Berners-Lee defined four foundational principles for Linked Data, which provide the guidelines for publishing and connecting data on the Web:

1. **Use URIs as names for things.** This principle advocates using URI references to identify not just Web documents and digital content, but also real-world objects and abstract concepts. A URI can identify a person, a place, a product, a concept — anything that needs to be referenced unambiguously. This goes beyond the traditional use of URIs as addresses for web pages.

2. **Use HTTP URIs, so that people can look up those names.** This principle advocates the use of HTTP URIs to identify objects and abstract concepts, enabling these URIs to be **dereferenced** (i.e., looked up) over the HTTP protocol into a description of the identified object or concept. When someone clicks on or requests an HTTP URI, they should get back useful information about the thing it identifies.

3. **When someone looks up a URI, provide useful information, using the standards (RDF, SPARQL).** This principle advocates using a single data model for publishing structured data on the Web — the Resource Description Framework (RDF). When a URI is dereferenced, the returned information should be in a machine-readable format (such as RDF) so that it can be automatically processed, integrated, and reasoned over.

4. **Include links to other URIs, so that they can discover more things.** This principle advocates the use of typed hyperlinks to connect not only Web documents, but any type of thing. Hyperlinks in the Linked Data context are called **RDF links** in order to distinguish them from hyperlinks between classic Web documents. These links enable both humans and machines to navigate from one data source to another, discovering related information across different datasets.

### 6.3 The Linked Open Data Cloud

The **Linked Open Data Cloud** is a visual representation of the datasets that have been published according to Linked Data principles and are interlinked with each other. The cloud diagram, available at [http://lod-cloud.net/](http://lod-cloud.net/), shows hundreds of datasets organized by domain, including:

- **Cross Domain:** General-purpose datasets like DBpedia and Wikidata that cover a wide range of topics.
- **Geography:** Geospatial datasets including national mapping agencies and gazetteers.
- **Government:** Open government data from various countries and regions.
- **Life Sciences:** Biomedical and biological datasets such as UniProt, ChEMBL, and Gene Ontology.
- **Linguistics:** Lexical and linguistic datasets including WordNet variants and lexicons.
- **Media:** Media-related datasets from organizations like the BBC.
- **Publications:** Academic and bibliographic datasets like DBLP and CiteSeer.
- **Social Networking:** Social data and user-generated content.
- **User Generated:** Community-contributed datasets.

The LOD Cloud demonstrates the power and scalability of the Linked Data approach: by following a common set of principles and using shared identifiers and data models, datasets from completely different domains can be connected, enabling cross-domain queries and knowledge discovery that would be impossible with isolated data silos.

---

## References

- **W3C (2014).** RDF 1.1 Concepts and Abstract Syntax – W3C Recommendation 25 February 2014. [https://www.w3.org/TR/rdf11-concepts/](https://www.w3.org/TR/rdf11-concepts/)
- **W3C (2014).** RDF 1.1 Semantics – W3C Recommendation 25 February 2014. [https://www.w3.org/TR/rdf11-mt/](https://www.w3.org/TR/rdf11-mt/)
- **W3C (2014).** RDF 1.1 Primer – W3C Working Group Note 24 June 2014. [https://www.w3.org/TR/rdf11-primer/](https://www.w3.org/TR/rdf11-primer/)
- **W3C (2013).** SPARQL 1.1 Query Language – W3C Recommendation 21 March 2013. [https://www.w3.org/TR/sparql11-query/](https://www.w3.org/TR/sparql11-query/)
- **Heath, T. and Bizer, C.** (2011). *Linked Data: Evolving the Web into a Global Data Space.* Morgan & Claypool Publishers. [http://linkeddatabook.com/editions/1.0/](http://linkeddatabook.com/editions/1.0/)
