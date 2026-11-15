# Activity 14.3 — SMTP Email and Credential Analysis with NetworkMiner

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 14  
> **Environment:** forenseWin VM  
> **Status:** Completed

## 1. Objective

Analyze SMTP authentication artifacts in network traffic using NetworkMiner.

The activity focuses on the Credentials tab, where the application presents authentication information extracted from supported protocols.

The evidence identifies an SMTP account:

```text
gurpartap@patriots.in
```

The exercise demonstrates that SMTP authentication data can be exposed in a packet capture when the authentication exchange is not protected by encryption.

The objective is to understand how credentials can be recovered from recorded network traffic and why plaintext or merely encoded authentication data presents a security risk.

The password is intentionally redacted in this public documentation.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseWin` |
| Operating System | Windows |
| Network Forensic Tool | NetworkMiner |
| Input Artifact | SMTP-related PCAP supplied by the course |
| Main Interface Tab | Credentials |
| Protocol | SMTP |
| Authentication Mechanism | SMTP AUTH LOGIN |
| Identified Account | `gurpartap@patriots.in` |
| Password | Redacted in public documentation |
| Analysis Type | Offline credential artifact examination |

The exact filename of the SMTP packet capture is not preserved in the supplied activity summary.

## 3. SMTP and Authentication Concepts

### Simple Mail Transfer Protocol

SMTP is used to transfer email messages between mail clients and servers and between mail transfer agents.

Depending on the server configuration, SMTP can support authentication before accepting a message for delivery.

### SMTP AUTH

SMTP AUTH extends the SMTP protocol with authentication mechanisms.

One commonly encountered mechanism is:

```text
AUTH LOGIN
```

In this exchange, the server requests a username and then a password.

The client sends the corresponding authentication data.

### Base64 Encoding

Some SMTP authentication exchanges use Base64 to represent the username and password.

Base64 is an encoding scheme, not an encryption mechanism.

It transforms binary data into printable text characters but does not provide confidentiality.

Anyone with access to an unprotected capture can decode the authentication values.

### NetworkMiner Credentials Tab

NetworkMiner can identify and display supported credentials extracted from packet captures.

The Credentials tab presents authentication artifacts in a consolidated view.

This can help the analyst identify:

- The protocol.
- The username.
- The authentication information available in the capture.
- Other related credential metadata.

The exact fields depend on the protocol and the data recovered.

## 4. Procedure

### Step 1 — Open the SMTP Packet Capture

The Windows forensic workstation was accessed.

NetworkMiner was opened.

The SMTP-related packet capture supplied by the course was loaded into the application.

NetworkMiner processes the PCAP and searches for supported network artifacts.

The filename of this particular capture was not included in the supplied activity summary.

### Step 2 — Allow NetworkMiner to Process the Capture

After loading the evidence, NetworkMiner analyzes the available packets.

The application identifies supported hosts, sessions, files, and authentication artifacts.

The availability of credentials depends on whether the relevant authentication exchange is present in the packet capture and whether it can be interpreted by the tool.

### Step 3 — Open the Credentials Tab

The **Credentials** tab was selected.

The application displayed credentials identified in the analyzed traffic.

The recorded evidence identifies the following SMTP account:

```text
gurpartap@patriots.in
```

The associated authentication information was also available in the tab.

The password is not reproduced in this README because this documentation is intended for a public GitHub repository.

### Step 4 — Examine the SMTP Authentication Evidence

The credential record was examined in the NetworkMiner interface.

The evidence demonstrates that authentication data associated with SMTP was recoverable from the captured network traffic.

An SMTP AUTH LOGIN exchange can contain messages similar to the following:

```text
AUTH LOGIN
334 <Base64-encoded username prompt>
<Base64-encoded username>
334 <Base64-encoded password prompt>
<Base64-encoded password>
235 Authentication succeeded
```

The values are encoded in Base64 in this example format.

The actual credential values should be preserved only in the controlled evidence file when required by the forensic exercise.

## 5. Expected Results

The activity demonstrates the recovery of SMTP authentication artifacts from a network capture.

| Item | Result |
|---|---|
| Tool | NetworkMiner |
| Interface Tab | Credentials |
| Protocol | SMTP |
| Authentication | AUTH LOGIN |
| Recovered Username | `gurpartap@patriots.in` |
| Password | Redacted in public documentation |
| Evidence Type | Network authentication artifact |

The result demonstrates that authentication information can be exposed when captured traffic does not provide adequate confidentiality.

## 6. Technical Analysis

### Why SMTP Authentication Can Expose Credentials

SMTP authentication mechanisms may transmit credentials in a representation that is readable or easily decoded.

The `AUTH LOGIN` exchange can use Base64 to encode the username and password.

Base64 does not encrypt the information.

If the network session is not protected by TLS or another appropriate encryption mechanism, someone with access to the packet capture may be able to recover the authentication data.

### Encoding Is Not Encryption

The difference is important:

| Mechanism | Purpose |
|---|---|
| Base64 | Represents data using printable characters |
| Encryption | Protects confidentiality through cryptographic transformation and key management |
| TLS | Protects data in transit between communicating endpoints |

A Base64 value should not be treated as protected merely because the original text is no longer immediately readable.

### NetworkMiner as a Forensic Tool

NetworkMiner presents supported credentials in a dedicated interface.

This helps the analyst identify authentication artifacts without manually decoding every packet.

However, the original packet capture remains the underlying evidence.

The analyst should correlate the NetworkMiner result with the corresponding packets and session details.

### SMTP and TLS

SMTP can use TLS to protect authentication and message content.

When a session is encrypted correctly, passive inspection of the packet capture should not expose the application credentials in the same manner as an unprotected exchange.

Security controls should therefore prioritize encrypted transport and the use of secure authentication mechanisms.

### Credential Handling in Forensic Reports

Credentials recovered from packet captures are sensitive evidence.

A public report should not unnecessarily disclose a working password.

The account identifier can be documented where it is relevant to the exercise, while the password should be redacted in public material.

The original capture and any unredacted evidence should be stored with appropriate access controls.

## 7. Results and Interpretation

The activity demonstrates that NetworkMiner can identify SMTP authentication artifacts in a packet capture and present them in the Credentials tab.

The recovered record identifies:

```text
gurpartap@patriots.in
```

The associated authentication information shows that the captured SMTP exchange exposed credential material.

This demonstrates the forensic importance of examining authentication protocols and verifying whether traffic was protected by encryption.

The password is intentionally omitted from this public README.

## 8. Concepts Practiced

- SMTP
- SMTP AUTH
- AUTH LOGIN
- NetworkMiner
- PCAP analysis
- Credential extraction
- Authentication artifacts
- Base64 encoding
- Difference between encoding and encryption
- TLS
- Cleartext credential exposure
- Network evidence correlation
- Sensitive evidence handling
- Password redaction

## 9. Evidence

**Required screenshot: Print 4 — PDF page 3.**

The screenshot should display NetworkMiner with the **Credentials** tab selected.

The evidence should show:

- The SMTP protocol.
- The recovered account `gurpartap@patriots.in`.
- The associated authentication record.

The password should be obscured in any additional public screenshot or documentation.

[View Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 14.3 is on page 3 of the consolidated PDF.

## References

- [RFC 4954 — SMTP Service Extension for Authentication](https://www.rfc-editor.org/rfc/rfc4954)
- [RFC 4648 — The Base16, Base32, and Base64 Data Encodings](https://www.rfc-editor.org/rfc/rfc4648)
- [NetworkMiner — Official Website](https://www.netresec.com/?page=NetworkMiner)
- [NetworkMiner — Security Onion Documentation](https://docs.securityonion.net/en/3/main/networkminer/)
- [Network Traffic Analysis for Incident Response — Credential Capture](https://www.infosecinstitute.com/resources/incident-response-resources/network-traffic-analysis-for-ir-credential-capture/)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 14.4](../atividade-14.4-wireshark-wifi/README.md)
