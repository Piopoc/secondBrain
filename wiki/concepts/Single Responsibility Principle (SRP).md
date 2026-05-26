---
date: 2026-05-23
source: [[WA]]
tags: [concept, architecture, design-principle]
---
# Single Responsibility Principle (SRP)

The "S" in SOLID. Every class/module should have **only one reason to change** — a single, well-defined responsibility.

SRP is a class-level formulation of the broader Separation of Concerns principle. While SoC divides an application into architectural layers (presentation, business, data), SRP applies the same idea at the granularity of individual classes.

**Examples from the WA stack:**
- [[DAO Pattern]]: Encapsulates *only* data access logic, keeping persistence separate from business rules.
- [[MVC Architectural Pattern]]: Separates Model (data), View (UI), and Controller (logic) so each component has exactly one job.
- [[Java Servlet]] as Controller: Handles requests and coordinates flow, but delegates DB access to DAOs and rendering to JSPs.

**The other SOLID principles** (not detailed here):
- **O** — Open/Closed Principle (OCP): Open for extension, closed for modification.
- **L** — Liskov Substitution Principle (LSP): Subtypes must be substitutable for their base types.
- **I** — Interface Segregation Principle (ISP): Many specific interfaces are better than one general-purpose interface.
- **D** — Dependency Inversion Principle (DIP): Depend on abstractions, not on concretions.
