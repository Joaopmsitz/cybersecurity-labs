# <img src="./images/web-requests.jpg" width="36" alt="Web Requests"> Web Requests

> HTB Academy — Cracking into Hack the Box

## Overview

Web Requests introduces HTTP communication between clients and web applications. Understanding requests and responses supports application testing, troubleshooting, and security analysis.

## Core Concepts

- **Methods:** GET, POST, PUT, PATCH, DELETE, HEAD, and OPTIONS.
- **Status codes:** 2xx success, 3xx redirection, 4xx client errors, and 5xx server errors.
- **Headers:** Host, Content-Type, Cookie, and Authorization.
- **Parameters:** query strings, form fields, and JSON request bodies.
- **Cookies and sessions:** state maintained across requests.
- **Content types:** formats such as `application/json` and `application/x-www-form-urlencoded`.

## Command Reference

| Objective | Example | Purpose |
|---|---|---|
| Inspect response | `curl -i https://<lab-target>/` | Displays headers and body |
| Save response separately | `curl -s -D headers.txt -o body.html https://<lab-target>/` | Separates headers and content |
| Send a custom header | `curl -H "X-Test: value" https://<lab-target>/` | Adds a request header |
| Send JSON | `curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' https://<lab-target>/api` | Sends a JSON body |
| Follow redirects | `curl -L https://<lab-target>/` | Follows HTTP redirects |

Use these examples only with authorized lab targets.

## Practical Workflow

1. Identify the URL and HTTP method.
2. Inspect request headers and parameters.
3. Send the request and analyze its status code.
4. Examine the response headers and body.
5. Change one input at a time and compare responses.
6. Record the evidence and conclusions.

## Lab Notes

Add exercise-specific findings and screenshots as you document the Academy labs.

## Completion

<a href="https://academy.hackthebox.com/achievement/badge/b81cf959-cf9a-11f0-9254-bea50ffe6cb4"><img src="./images/htb-web-requests-badge.png" width="120" alt="HTB Academy — Your request is my demand Badge"></a>

**Completed:** 2 December 2025

## References

- [HTB Academy — Web Requests](https://academy.hackthebox.com/app/module/35)
- [MDN — HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
