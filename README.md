# HTTP Server Project Writeup — Multithreaded HTTP/1.0 Web Server - NO CODE

## High-level description

This project implements a **HTTP/1.0 web server** that listens on a TCP port, parses incoming HTTP requests, and serves content from a structured document root (e.g., `http-root-dir`). It supports both **static content** (HTML/images/files) and **dynamic content** via **CGI**, along with directory browsing and multiple concurrency models. The emphasis is on correct HTTP request/response behavior, robust file serving, and scalable request handling under concurrent clients.

## Course / policy note

Completed for **Purdue CS252 (Spring 2025)**. Source code is **not publicly available** in order to respect course and academic integrity policies.

## Implemented functionality

### Core HTTP handling
- Parses HTTP request lines and headers (HTTP/1.0)
- Handles **GET** requests end-to-end (status codes + headers + body)
- Serves static files from the configured document root (e.g., `http-root-dir/htdocs`)

### Directory browsing
- If a requested path is a directory, returns an HTML directory listing with navigable links
- Supports sorting directory listings by:
  - name
  - size
  - last modified time

### CGI execution
- Executes CGI programs from `http-root-dir/cgi-bin`
- **GET CGI support:** passes query parameters through the appropriate CGI mechanism and returns script output to the client

### Authentication
- Implements **HTTP Basic Authentication** to restrict access (browser prompts for credentials when missing/invalid)

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
  - Reads POST request bodies
  - Pipes POST content to the CGI program’s `stdin`
  - Sets correct `CONTENT_LENGTH` for the CGI environment
- **Robustness with real applications**
  - Validated behavior with real browsers (including **Google Chrome**) and higher-stress request patterns

## Testing notes (brief)
- Tested using `curl` and browser-based requests
- Verified static file serving, directory listing behavior, authentication, CGI GET/POST, and each concurrency mode
