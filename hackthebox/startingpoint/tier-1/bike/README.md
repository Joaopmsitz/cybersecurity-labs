# Bike — Starting Point (Very Easy)

**Operating System:** Linux  
**Technologies:** Node.js, Express, Handlebars  
**Status:** Completed

## Completion Proof

[View Hack The Box Achievement](https://labs.hackthebox.com/achievement/machine/2578759/449)

## What I Practiced

- Network scanning and service enumeration with Nmap.
- Identification of SSH on TCP port 22 and HTTP on TCP port 80.
- Web application fingerprinting to identify Node.js and Express.
- Identification of the Handlebars template engine.
- Testing for Server-Side Template Injection (SSTI).
- Analysis of template evaluation and unsafe server-side input handling.
- URL encoding of special characters using Burp Suite Decoder.
- Exploitation of SSTI to achieve remote command execution.
- Retrieval of the machine flag after successful exploitation.

## Key Takeaways

- Server-Side Template Injection occurs when untrusted input is evaluated as template syntax.
- Template engines should not process user-controlled input as executable template expressions.
- SSTI can escalate from template evaluation to remote code execution, depending on the engine and application configuration.
- Input handling, template rendering, and execution privileges should be designed securely.
- Web server processes should run with the least privileges necessary to perform their tasks.
- Security testing should identify both the initial vulnerability and its potential impact.

---

[Back to Tier 1](../README.md) · [Back to Starting Point](../../README.md) · [Back to Hack The Box](../../../README.md)
