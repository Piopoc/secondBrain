# Fetch API

The **Fetch API** is a modern interface for making asynchronous HTTP requests in the browser. It provides a more powerful and flexible alternative to `XMLHttpRequest`.

## Key Features
- **Promise-Based:** Uses JavaScript Promises, allowing for cleaner asynchronous code using `async/await`.
- **Stream-Based:** Provides a `Response` object that allows for streaming the body.
- **Simplified Syntax:** A simple `fetch(url)` call initiates a GET request.

## Workflow
A typical fetch operation follows two steps:
1. **Check Status:** Verify if the response was successful (e.g., `response.ok`).
2. **Parse Body:** Convert the response body into a usable format (e.g., `response.json()`).
