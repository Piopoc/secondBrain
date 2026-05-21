# Server-Side Validation

**Server-Side Validation** is the process of validating submitted data on the web server before it is processed or stored in a database.

## Importance
It is the **last line of defense**. Because client-side validation can be bypassed, the server must independently verify all incoming data to prevent:
- **Data Corruption:** Incorrect formats entering the database.
- **Security Vulnerabilities:** Malicious payloads (SQLi, XSS) reaching the backend.

## Trade-off
Unlike client-side validation, it requires a network round-trip, which can make the user experience feel slower if not implemented with AJAX.
