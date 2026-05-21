# XMLHttpRequest

The **XMLHttpRequest (XHR)** object is the traditional browser API used to send HTTP requests to a server and receive data asynchronously.

## Request-Response Cycle
An XHR request consists of:
- **Request:** Method (GET, POST, etc.), URL, Headers, and an optional Body.
- **Response:** Status code (e.g., 200 OK), Response Headers, and the Response Body.

## State Management
The `readyState` property tracks the progress of the request:
- `0`: Uninitialized
- `1`: Loading
- `2`: Loaded (headers received)
- `3`: Interactive (body receiving)
- `4`: Complete (`XMLHttpRequest.DONE`)

## Modern Alternatives
While XHR is still supported, the **Fetch API** has largely replaced it in modern development due to its cleaner, Promise-based syntax.
