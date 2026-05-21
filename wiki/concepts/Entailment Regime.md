# Entailment Regime

An **Entailment Regime** is a set of rules that defines how a system can perform logical inference over RDF data. It specifies which new triples can be derived from a given set of existing triples.

## Purpose
Because the Semantic Web allows anyone to create new vocabularies, different types of reasoning are needed. An entailment regime provides the formal semantics for a specific kind of reasoning.

## Example: RDFS Entailment
The **RDFS (RDF Schema)** entailment regime allows a system to infer types. For example, if a property `foaf:knows` has a domain of `foaf:Person`, and the triple `ex:bob foaf:knows ex:alice` exists, the system can infer that `ex:bob` is a `foaf:Person`.
