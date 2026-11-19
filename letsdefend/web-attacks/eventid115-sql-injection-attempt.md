# SQL Injection Attempt Detected

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 115 |
| Detection Rule | SOC165 - Possible SQL Injection Payload Detected |
| Event Time | 2022-02-25 11:34 |
| Severity | High |
| Category | Web Attack |
| Hostname | WebServer1001 |
| Source IP | 167.99.169.17 |
| Destination IP | 172.16.17.18 |
| HTTP Method | GET |
| Target | `/search/` |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

A web attack alert was generated after a GET request containing a SQL injection payload was detected against the `/search/` endpoint of `WebServer1001`.

The investigation focused on analyzing the requested URLs, decoding the payloads, reviewing HTTP responses, and determining whether the attack successfully altered application behavior.

The available logs confirmed multiple SQL injection attempts, but did not establish successful exploitation.

## 3. Evidence Analysis

### Suspicious Request

The original request contained the following URL-encoded payload:

```text
https://172.16.17.18/search/?q=%22%20OR%201%20%3D%201%20--%20-
```

Decoded:

```sql
" OR 1 = 1 -- -
```

Additional requests included authentication-bypass and SQL query-manipulation patterns, such as:

```sql
' OR 'x'='x
1' ORDER BY 3--+
```

### HTTP Response Analysis

SIEM logs showed multiple requests to the affected application.

The investigated SQL injection requests returned:

| HTTP Status | Response Size | Assessment |
|---|---:|---|
| 500 | 948 bytes | Internal Server Error |

Normal application requests returned HTTP 200 responses.

The repeated HTTP 500 responses did not indicate successful query manipulation or authentication bypass.

### Source Reputation

The source IP `167.99.169.17` was identified as suspicious by external reputation sources.

The endpoint investigation did not identify evidence of successful exploitation.

### External References

- [Independent EventID 115 investigation](https://www.policytopackets.com/writeups/letsdefend/soc/165_115/)
- [Additional SOC165 walkthrough](https://octopus175.github.io/letsdefend/letsdefend-soc165/)

These sources provide additional context for the requested URLs, source IP, and HTTP response analysis.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1190 | Exploit Public-Facing Application | SQL injection attempts targeting the web application |

The technique represents the attempted exploitation. Successful application compromise was not established.

## 5. Response Actions

- Reviewed the alert and HTTP request metadata.
- Analyzed the suspicious SQL injection payloads.
- Decoded URL-encoded request parameters.
- Correlated requests with server response codes.
- Reviewed source IP reputation.
- Verified that exploitation was unsuccessful.
- Classified the alert as True Positive.

No containment or remediation action was documented in the original investigation.

## 6. Conclusion

The investigation confirmed a **True Positive SQL Injection attempt** targeting the search endpoint of `WebServer1001`.

Multiple malicious requests were identified, but the server returned HTTP 500 responses instead of evidence of successful query manipulation or unauthorized access.

**Final Verdict: True Positive**

**Impact Assessment: SQL Injection Attempt - No Confirmed Exploitation**
