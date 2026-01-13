# Multithreaded Web Server (HTTP/1.0)

## Overview
This project implements a small web server that listens on a TCP port, interprets basic HTTP/1.0 requests, and serves content from a configurable document root. The focus is on correct request/response behavior, safe file serving, and handling multiple clients concurrently.

## Capabilities (High Level)
- **HTTP request handling:** accepts connections, parses requests and headers, and returns well-formed HTTP responses (status line, headers, body).
- **Static content serving:** delivers common file types from a document root while enforcing path safety (e.g., preventing unintended filesystem access).
- **Dynamic content execution:** supports running server-side programs/scripts and returning their output as HTTP responses.
- **Access control:** supports an authentication mechanism to restrict access to protected resources.
- **Concurrency options:** explores multiple models for handling simultaneous clients, including single-threaded and multi-worker approaches.
- **Observability:** includes basic operational visibility such as request logging and a lightweight status view for runtime metrics.

### Concurrency modes
Supports four server modes:
- **Iterative** (single request at a time)
- **Fork-per-request**
- **Thread-per-request**
- **Thread pool** (fixed pool of worker threads)

### Stats & logging pages
- Server **stats page** exposing runtime/server information (uptime, request counts, service-time min/max, etc.)
- Persistent **request logging** and a page to view logs via the browser

## Extra credit
- **Full POST support for CGI**

## What I Learned
- **Networking fundamentals:** TCP accept loops, connection lifecycles, and dealing with partial reads/writes.
- **HTTP correctness:** how small protocol details (headers, status codes, content length, and encoding assumptions) affect real clients.
- **Secure file serving:** validating paths and handling filesystem edge cases safely.
- **Concurrency tradeoffs:** differences in latency, throughput, resource usage, and failure isolation across process/thread models.
- **Robustness under load:** why servers must handle malformed inputs, slow clients, and high request churn without crashing or corrupting state.

## Testing notes (brief)
- Tested using `curl` and browser-based requests
- Verified static file serving, directory listing behavior, authentication, CGI GET/POST, and each concurrency mode

## Notes
This repository intentionally omits implementation details that would function as a step-by-step solution. It is meant to document scope and learning outcomes rather than provide a reference implementation.

