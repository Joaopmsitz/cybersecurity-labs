# JavaScript Code Detected in URL

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 116 |
| Detection Rule | SOC166 - Javascript Code Detected in Requested URL |
| Event Time | 2022-02-26 18:56 |
| Severity | Medium |
| Category | Web Attack |
| Hostname | WebServer1002 |
| Source IP | 112.85.42.13 |
| Destination IP | 172.16.17.17 |
| HTTP Method | GET |
| Target | `/search/` |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

A web attack alert was generated after suspicious JavaScript code was identified in a requested URL targeting `WebServer1002`.

The investigation focused on validating the payload, correlating HTTP requests, and reviewing server responses to determine whether the activity resulted in successful Cross-Site Scripting (XSS) exploitation.

The available evidence confirmed an XSS attempt, but did not establish successful JavaScript execution or server compromise.

## 3. Evidence Analysis

### Suspicious Request

The alert identified the following request:

```text
https://172.16.17.17/search/?q=<$script>javascript:$alert(1)<$/script>
```

The payload attempted to inject JavaScript through the `q` search parameter.

### Network Analysis

| Field | Value |
|---|---|
| Source IP | 112.85.42.13 |
| Destination IP | 172.16.17.17 |
| Hostname | WebServer1002 |
| HTTP Method | GET |

SIEM logs showed that ordinary application requests returned HTTP 200 responses, while suspicious XSS-related requests received HTTP 302 redirects.

The redirect behavior did not provide evidence that the injected JavaScript executed successfully.

### Source Reputation

The source IP was identified as suspicious by reputation sources, including AbuseIPDB.

The available endpoint and server analysis did not establish successful exploitation.

### External References

- [Independent EventID 116 investigation](https://www.policytopackets.com/writeups/letsdefend/soc/166_116/)
- [Additional SOC166 analysis](https://github.com/Fooster171/LetsDefend-Writeups/wiki/SOC166-Javascript-Code-Detected-in-Requested-URL)

These sources corroborate the source IP, target server, suspicious request, and HTTP 302 responses.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1190 | Exploit Public-Facing Application | XSS payload sent to a web application endpoint |

This mapping represents the attempted exploitation. The available evidence did not confirm successful client-side JavaScript execution.

## 5. Response Actions

- Reviewed the alert and suspicious URL.
- Analyzed the JavaScript injection payload.
- Correlated source and destination IP addresses.
- Reviewed HTTP response codes and request behavior.
- Checked source IP reputation.
- Verified that successful exploitation was not established.
- Classified the alert as True Positive.

Input validation, output encoding, and web application security controls were identified as relevant recommendations.

## 6. Conclusion

The investigation confirmed a **True Positive XSS attempt** targeting the search endpoint of `WebServer1002`.

The attacker submitted JavaScript payloads through the URL, but the requests received HTTP 302 redirects. No evidence established successful script execution or compromise of the web application.

**Final Verdict: True Positive**

**Impact Assessment: XSS Attempt - No Confirmed Exploitation**
