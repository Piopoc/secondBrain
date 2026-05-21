# Cross-Origin Resource Sharing (CORS)

**CORS (Cross-Origin Resource Sharing)** is a security mechanism that allows a web browser to request resources from a domain different from the one that served the current page.

## Same-Origin Policy
By default, browsers enforce the **Same-Origin Policy**, which prevents a script on one domain from accessing data on another domain to prevent malicious attacks (like CSRF).

## How CORS Works
CORS uses specific HTTP headers to relax this restriction. The server specifies which origins are permitted to access its resources via headers like `Access-Control-Allow-Origin`. If the origin of the requesting page is in the allowed list, the browser permits the request.
