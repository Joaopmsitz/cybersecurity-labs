# Web Attack Investigations

Documented investigations involving malicious HTTP requests, SQL injection attempts, and client-side script injection.

## Investigations

| Event ID | Detection Rule | Investigation Report | Verdict |
|---:|---|---|---|
| 115 | SOC165 | [SQL Injection Attempt Detected](./eventid115-sql-injection-attempt.md) | True Positive |
| 116 | SOC166 | [JavaScript Code Detected in URL](./eventid116-javascript-code-detected.md) | True Positive |

## Investigation Highlights

### EventID 115 - SQL Injection

A malicious SQL injection payload was submitted to the `/search/` endpoint of WebServer1001. The requests received HTTP 500 responses, and successful exploitation was not confirmed.

### EventID 116 - Cross-Site Scripting

JavaScript injection attempts were observed against the `/search/` endpoint of WebServer1002. The suspicious requests received HTTP 302 redirects, with no evidence of successful script execution.

## Topics Covered

- HTTP request analysis
- SQL injection detection
- Cross-Site Scripting attempts
- URL payload decoding
- Server response analysis
- Exploitation and impact validation

## Scope

These reports document simulated LetsDefend training scenarios. Findings and response actions should not be interpreted as real-world incident response engagements.

[Back to LetsDefend](../README.md)
