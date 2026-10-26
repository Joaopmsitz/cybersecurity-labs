# Activity 9.08 — Verifying Web Certificates with OCSP on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 35–36  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Use OpenSSL on Kali Linux to analyze web server digital certificates and examine OCSP (Online Certificate Status Protocol) information during a TLS connection.

## Environment

- **Operating system:** Kali Linux
- **Tool:** OpenSSL
- **Command:** `openssl s_client`
- **Servers analyzed:** `www.grancursos.com.br` and `www.google.com`
- **Port:** 443 (HTTPS)

> Credentials used to access the lab environment are not recorded in this README.

## 1. Opening the Terminal

A terminal was opened on Kali Linux, and administrative access was obtained using:

```bash
sudo -i
```

The directory used in the activities was then accessed:

```bash
cd /home/aluno/Documentos/Arquivos
```

## 2. Checking the Server Certificate

To establish a TLS connection to the Gran Cursos server and request OCSP status information, the following command was executed:

```bash
openssl s_client -connect www.grancursos.com.br:443 -status
```

The `-connect` option specifies the server and port used for the connection, while `-status` requests an OCSP stapling response from the server, when available.

Relevant portion of the output:

```text
Connecting to 172.67.175.92
CONNECTED(00000003)
depth=2 C=US, O=Google Trust Services LLC, CN=GTS Root R4
verify return:1
depth=1 C=US, O=Google Trust Services, CN=WE1
verify return:1
depth=0 CN=grancursos.com.br
verify return:1
```

The certificate chain was validated during the connection.

## 3. Analyzing the OCSP Response

The command output included an OCSP response:

```text
OCSP response:
======================================
OCSP Response Data:
    OCSP Response Status: successful (0x0)
    Response Type: Basic OCSP Response
    Version: 1 (0x0)
    Responder Id: 9077923567C4FFA8CCA9E67BD980797BCC93F938
    Produced At: Dec  2 17:35:25 2025 GMT
    Responses:
    Certificate ID:
      Hash Algorithm: sha1
      Issuer Name Hash: B9BED5F1A61E40B24196B0C29E7E1A9D8BFCB520
      Issuer Key Hash: 9077923567C4FFA8CCA9E67BD980797BCC93F938
      Serial Number: B57B7C7121C597FB1328D77A02E8828B
    Cert Status: good
    This Update: Dec  2 17:35:25 2025 GMT
    Next Update: Dec  9 16:35:24 2025 GMT

    Signature Algorithm: ecdsa-with-SHA256
```

The field:

```text
Cert Status: good
```

indicates that, according to the OCSP response returned during the lab, the certificate was reported as not revoked at that time.

The `This Update` and `Next Update` fields were also observed. They indicate the update time associated with the response and the time by which newer status information is expected.

## 4. Analyzing the Certificate Chain and TLS Connection

The output also displayed the certificate chain:

```text
Certificate chain
 0 s:CN=grancursos.com.br
   i:C=US, O=Google Trust Services, CN=WE1
   a:PKEY: EC, (prime256v1); sigalg: ecdsa-with-SHA256
   v:NotBefore: Nov 27 15:16:12 2025 GMT; NotAfter: Feb 25 16:14:52 2026 GMT
 1 s:C=US, O=Google Trust Services, CN=WE1
   i:C=US, O=Google Trust Services LLC, CN=GTS Root R4
   a:PKEY: EC, (prime256v1); sigalg: ecdsa-with-SHA384
   v:NotBefore: Dec 13 09:00:00 2023 GMT; NotAfter: Feb 20 14:00:00 2029 GMT
 2 s:C=US, O=Google Trust Services LLC, CN=GTS Root R4
   i:C=BE, O=GlobalSign nv-sa, OU=Root CA, CN=GlobalSign Root CA
   a:PKEY: EC, (secp384r1); sigalg: sha256WithRSAEncryption
   v:NotBefore: Nov 15 03:43:21 2023 GMT; NotAfter: Jan 28 00:00:42 2028 GMT
```

The following TLS connection parameters were also identified:

```text
subject=CN=grancursos.com.br
issuer=C=US, O=Google Trust Services, CN=WE1

Peer signing digest: SHA256
Peer signature type: ecdsa_secp256r1_sha256
Negotiated TLS1.3 group: X25519MLKEM768

Verification: OK

New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 256 bit

Verify return code: 0 (ok)
```

These details make it possible to examine the certificate presented by the server, its issuing authority, the TLS version used, and the negotiated cryptographic suite.

## 5. Checking OCSP on Google

A second test was performed using Google's server:

```bash
openssl s_client -connect www.google.com:443 -status
```

The relevant output was:

```text
Connecting to 192.178.155.106
CONNECTED(00000003)
depth=2 C=US, O=Google Trust Services LLC, CN=GTS Root R1
verify return:1
depth=1 C=US, O=Google Trust Services, CN=WR2
verify return:1
depth=0 CN=www.google.com
verify return:1
OCSP response: no response sent
```

In this case, the message:

```text
OCSP response: no response sent
```

indicates that the server did not send an OCSP stapling response during this connection.

This does not, by itself, mean that the certificate was invalid or revoked. It only indicates that an OCSP stapling response was not provided in this connection.

## Evidence — Step 5

Required caption before the screenshot:

> Screenshot for Activity 9.8: the result of the HTTPS connection to `www.google.com` using `openssl s_client -status`, showing the message `OCSP response: no response sent`.

Evidence for this activity is included in the PDF for Module 9, Classes 35–36.

[View Evidence — Classes 35–36](../evidencias.pdf)

## Activity Workflow

| Stage | Result |
|---|---|
| TLS connection | `openssl s_client` |
| OCSP stapling request | `-status` option |
| Gran Cursos | OCSP response containing `Cert Status: good` |
| Google | `OCSP response: no response sent` |

## Result

HTTPS certificates were analyzed using OpenSSL and `s_client`. The activity demonstrated both an OCSP response reporting `good` and a connection in which no OCSP stapling response was sent.

The results also provided an opportunity to inspect the certificate chain, validity information, TLS protocol version, and negotiated cryptographic parameters.

---

[Back to Classes 35–36](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
