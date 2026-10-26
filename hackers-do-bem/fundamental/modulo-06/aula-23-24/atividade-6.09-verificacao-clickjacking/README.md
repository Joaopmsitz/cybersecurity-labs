# Activity 6.09 — Checking Websites for Clickjacking Vulnerabilities

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 23–24  
> **Environment:** Local computer and web browser  
> **Status:** Completed

## Objective

This activity used the Clickjacker service to inspect the clickjacking protections configured on different websites.

The analysis focused primarily on the following HTTP security headers and directives:

- `X-Frame-Options`
- `Content-Security-Policy`, specifically the `frame-ancestors` directive

The objective was to compare the configurations reported by the service and determine whether the tested websites had mechanisms to restrict embedding in iframes.

## Environment

- **System:** Local computer
- **Browser:** Web browser
- **Service:** Clickjacker
- **URL:** `https://clickjacker.io/`

The local computer was used for this activity rather than the AWS virtual machine.

## 1. Access Clickjacker

The browser was opened, and the following address was accessed:

```text
https://clickjacker.io/
```

The website provides a field for entering the site to be analyzed and displays information related to clickjacking protections.

The information presented includes:

- **IP Address:** The IP address associated with the tested website.
- **Time:** The time when the test was performed.
- **X-Frame-Options:** An HTTP response header used to control whether a page can be loaded in a frame or iframe.
- **CSP Header (Frame-Ancestors):** Information about the `frame-ancestors` directive in the Content Security Policy (CSP).

## 2. Understand the Protection Mechanisms

### X-Frame-Options

The `X-Frame-Options` HTTP response header controls whether a page can be embedded in a frame or iframe.

Two relevant values are:

**`DENY`**

Prevents the page from being embedded in frames.

**`SAMEORIGIN`**

Allows the page to be embedded only when the embedding page has the same origin, subject to the browser's enforcement of the policy.

The absence of this header does not, by itself, prove that a website is vulnerable, because other policies—particularly CSP—can also provide protection.

### CSP — `frame-ancestors`

The directive:

```text
frame-ancestors
```

is part of the Content Security Policy (CSP). It specifies which origins are permitted to embed a page in a frame or iframe.

This policy can provide an additional layer of protection against clickjacking.

When supported and correctly configured, `frame-ancestors` can restrict embedding to specified origins or prevent it entirely.

## 3. Test `esr.rnp.br`

In the **Test for Clickjacking now** field, the following website was entered:

```text
esr.rnp.br
```

The test returned:

```text
Test Results:
Site:
https://esr.rnp.br
IP Address:	177.136.78.45
Time:	Tue Sep 30 2025 00:35:08 GMT+0000 (Coordinated Universal Time)
X-Frame-Options: SAMEORIGIN
CSP Header (Frame-Ancestors)	Missing anti-framing policy
```

The result showed that the website returned the following policy:

```text
X-Frame-Options: SAMEORIGIN
```

This restricts embedding to pages with the same origin.

Although the CSP field reported:

```text
Missing anti-framing policy
```

the presence of `X-Frame-Options: SAMEORIGIN` provides an anti-framing protection mechanism.

Therefore, the absence of the `frame-ancestors` directive should not be interpreted in isolation as proof of a vulnerability.

## 4. Test `www.hackthissite.org`

The following website was tested next:

```text
www.hackthissite.org
```

Clickjacker displayed the following results:

```text
Test Results:
Site:	
https://www.hackthissite.org
IP Address:	137.74.187.100
Time:	Tue Sep 30 2025 00:37:18 GMT+0000 (Coordinated Universal Time)
X-Frame-Options:	Missing header
CSP Header (Frame-Ancestors)	Missing anti-framing policy
Total scans so far: 3,548,984
```

In this result, the service reported:

```text
X-Frame-Options: Missing header
```

and:

```text
CSP Header (Frame-Ancestors)	Missing anti-framing policy
```

In other words, the test did not identify an `X-Frame-Options` header or a `frame-ancestors` policy restricting the website's embedding.

Based on the laboratory's interpretation, this configuration was classified as potentially vulnerable to clickjacking.

**Important distinction:** The absence of these two protections indicates that the tested response did not expose those anti-framing controls. It does not, by itself, demonstrate a successful exploit or prove that an actual attack is possible in every context. This test inspected reported security policies; it did not perform an attack against users.

This is the step specified for the activity evidence.

## Comparison of Results

| Website | X-Frame-Options | CSP `frame-ancestors` | Observed result |
|---|---|---|---|
| `esr.rnp.br` | `SAMEORIGIN` | Missing | Protection provided by `X-Frame-Options` |
| `www.hackthissite.org` | Missing | Missing | Neither of these anti-framing policies was identified by the test |

The comparison demonstrates the importance of evaluating anti-framing protections together.

In the first case, even though the `frame-ancestors` directive was absent, the website had an `X-Frame-Options: SAMEORIGIN` policy.

In the second case, the service did not identify either mechanism.

These findings reflect the results recorded during the laboratory on September 30, 2025. Website configurations can change over time, so the results should not be treated as a statement about the websites' current security posture.

## Concepts Practiced

### Clickjacking

Clickjacking is a technique that can use overlapping elements or embedded content to trick a user into performing an action different from the one they believe they are performing.

One mitigation is to prevent pages from being embedded in frames by unauthorized origins.

### X-Frame-Options

This HTTP response header controls whether a page can be loaded inside a frame or iframe.

The laboratory observed two scenarios:

```text
SAMEORIGIN
```

and:

```text
Missing header
```

The `SAMEORIGIN` value restricts embedding to pages from the same origin, while a missing header means that this particular protection was not identified in the response.

### Content Security Policy (CSP)

CSP allows websites to define security policies for different types of content.

The directive:

```text
frame-ancestors
```

specifies which origins are allowed to embed the page in frames.

Unlike `frame-src`, which controls the frames a page can load, `frame-ancestors` controls which pages are allowed to embed the protected page.

### Anti-Framing Protections

Anti-framing policies restrict the ability of other pages to embed a website.

These policies are important for reducing the risk of clickjacking attacks. Correctly configured `X-Frame-Options` or CSP `frame-ancestors` directives can help mitigate this risk.

## Results

Two websites were analyzed using Clickjacker.

For the first website:

```text
esr.rnp.br
```

the service identified:

```text
X-Frame-Options: SAMEORIGIN
```

For the second website:

```text
www.hackthissite.org
```

the service reported that the following protections were missing:

```text
X-Frame-Options
```

and:

```text
CSP Header (Frame-Ancestors)
```

The activity demonstrated how HTTP response headers and CSP policies can be used to assess and mitigate risks associated with embedding web pages in iframes.

The results also reinforced that a missing header is an indicator to investigate rather than, by itself, conclusive proof of an exploitable vulnerability.

## Evidence

The evidence for this activity corresponds to **Step 4**, in which `www.hackthissite.org` was tested and the results for `X-Frame-Options` and `CSP Header (Frame-Ancestors)` were displayed.

[View Evidence — Classes 23–24](../evidencias.pdf)

---

[Back to Classes 23–24](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
