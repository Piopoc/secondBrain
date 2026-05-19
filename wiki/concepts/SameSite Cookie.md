---
date: 2026-05-18
source: [[WA - 11]]
tags: [security, cookies]
---
# SameSite Cookie
A cookie attribute that tells the browser whether to send cookies with cross-site requests. It is a primary defense against [[Cross-Site Request Forgery (CSRF)]].
- **Strict**: Cookie is only sent in a first-party context.
- **Lax**: Cookie is sent with top-level GET navigations.
- **None**: Cookie is sent with all requests (requires `Secure` attribute).
