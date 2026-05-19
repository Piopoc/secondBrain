---
date: 2026-05-18
source: [[WA - 11]]
tags: [html5, web-security, seo, frontend]
---
# HTML5 Semantics and Web Security Introduction

## Overview
Analysis of the modern web's structural foundation through [[wiki/concepts/HTML5]], focusing on the shift toward semantic markup for accessibility and [[SEO]], the mechanics of the [[Box Model]], and an introduction to the fundamental pillars of [[Web Security]].

## HTML5 Structure and Document Type
The structure of a web page is defined by its markup, starting with the **DOCTYPE**.
- **[[DOCTYPE]]**: A declaration that informs the browser about the document type and HTML version.
    - **HTML4**: Relied on complex Document Type Definitions ([[DTD]]).
    - **HTML5**: Uses a simplified marker: `<!DOCTYPE html>`.
- **[[XHTML]]**: A hybrid of XML and HTML, requiring stricter syntax.
- **Basic Page Skeleton**:
    - `<html>`: The root element.
    - `<head>`: Contains metadata, styles, and scripts (not visible to the user).
    - `<body>`: Contains the visible content of the page.

## Metadata and SEO
The `<meta>` element is used to provide additional information about the document.
- **[[SEO]] (Search Engine Optimization)**: The practice of optimizing a page to rank higher in search results.
    - **Keywords**: Largely ignored by modern search engines.
    - **Description**: Used by engines to generate the search snippet.
    - **Title**: High relevance for ranking; should reflect the site's hierarchical structure.
- **Best Practices**: Use accurate descriptions, hierarchical titles, and semantic HTML to assist crawlers.

## Semantic vs. Procedural Markup
The evolution of HTML has seen a shift from procedural to semantic markup.
- **[[Procedural Markup]]**: Describes *how* to render content (e.g., `<b>` for bold, `<i>` for italic).
- **[[Semantic Markup]]**: Describes *what* the content is (e.g., `<strong>` for importance, `<em>` for emphasis).
- **HTML5 Semantic Elements**: Introduce tags that define the role of a page section: `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, and `<footer>`.

## The Box Model and Layout
HTML rendering is based on the **[[Box Model]]**, a concept inherited from [[TeX]] (created by [[Donald Knuth]]).

### Block vs. Inline Elements
- **[[Block Element]]**: An HTML element that takes up the full width of its parent container and always starts on a new line (e.g., `<div>`, `<p>`, `<h1>`-`<h6>`, `<ul>`, `<li>`).
- **[[Inline Element]]**: An HTML element that only takes up as much width as necessary and does not force a new line (e.g., `<span>`, `<a>`, `<img>`, `<strong>`).
- **Constraint**: Nesting a block element inside an inline element is syntactically incorrect.

### Content Elements
- **Special Tags**: `<br>` (line break), `<hr>` (horizontal rule), `<sup>` (superscript), `<sub>` (subscript), `<s>` (strikethrough), and `<code>`.
- **Lists**:
    - Ordered (`<ol>`) and Unordered (`<ul>`) using `<li>`.
    - Definition lists (`<dl>`) using `<dt>` (term) and `<dd>` (description).
- **[[Hyperlink]]**: The `<a>` tag uses the `href` attribute to link to resources via [[Absolute URL]]s or [[Relative URL]]s. It supports various protocols (`http`, `mailto`, `ftp`, `tel`).
- **Media**: The `<img>` tag (inline) is used for images, often wrapped in `<figure>` and `<figcaption>` for accessibility.
- **Tables**: Structured using `<table>`, `<tr>` (rows), `<td>` (data), and `<th>` (headers).
- **Forms**: The `<form>` element manages user input via `action` and `method` (GET/POST). Inputs include `<input>` (various types), `<textarea>`, and `<select>`.

## Introduction to Web Security
Web security focuses on protecting applications from malicious attacks.

### The CIA Triad
The three fundamental pillars of cybersecurity are:
1. **[[Confidentiality]]**: Ensuring that data is accessible only to authorized users.
2. **[[Integrity]]**: Ensuring that data is not altered or tampered with.
3. **[[Availability]]**: Ensuring that services are accessible when needed.

### Security Frameworks and Risks
- **[[OWASP Top Ten]]**: The industry-standard list of the ten most critical web application security risks.
- **Attack Motivations**: Financial gain, espionage, hacktivism, or personal challenge.
- **Common Vulnerabilities**:
    - **[[SQL Injection]]**: Exploits poorly handled form inputs to execute unauthorized database queries.
    - **[[Cross-Site Scripting (XSS)]]**: Injects malicious scripts into the victim's browser.
        - **[[Stored XSS]]**: Script is permanently stored on the server.
        - **[[Reflected XSS]]**: Script is reflected via a URL parameter.
        - **[[DOM-based XSS]]**: Vulnerability exists in the client-side DOM manipulation.
    - **[[Cross-Site Request Forgery (CSRF)]]**: Forces an authenticated user to perform unwanted actions.

### Defenses
- **For SQL Injection**: Use [[Prepared Statements]].
- **For XSS**: Implement [[Output Encoding]], [[HTML Sanitization]], and a strong [[Content Security Policy (CSP)]].
- **For CSRF**: Use the [[SameSite Cookie]] attribute.
