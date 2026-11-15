# Activity 1.3 — Web Reconnaissance with FinalRecon

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Explore FinalRecon, an open-source web reconnaissance tool that automates information collection about web targets.

The activity introduces several reconnaissance capabilities used to identify information that can support security assessments and incident investigations.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Language | Python 3 |
| Tool | FinalRecon |
| Script Path | /opt/FinalRecon/finalrecon.py |
| Example Target | https://www.google.com |

## 3. Reconnaissance Capabilities

The original training material describes the following features:

| Feature | Purpose |
|---|---|
| WHOIS | Obtain domain registration information |
| HTTP Headers | Inspect HTTP response headers |
| SSL Information | Inspect SSL/TLS certificate information |
| DNS Enumeration | Identify DNS records |
| Subdomain Enumeration | Discover related subdomains |
| Traceroute | Inspect the network route to a destination |
| Directory Search | Identify discoverable web directories |
| Port Scanning | Identify accessible ports |
| Web Crawling | Analyze pages and links |

These capabilities can help identify exposed services, technology information, and potential areas requiring further investigation.

## 4. Procedure

### Step 1 — Display the Help Menu

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py -h
```

This command displays the tool's usage information and available options.

The assignment requires this step to be performed before testing the individual reconnaissance modules.

### Step 2 — Inspect SSL Information

Replace the example domain with a known website.

The supplied example is:

```bash
python3 /opt/FinalRecon/finalrecon.py --sslinfo --url https://www.google.com
```

The `--sslinfo` option invokes the SSL certificate information module.

The output can contain information associated with the certificate and its validity.

The actual output depends on the target website and the certificate presented at execution time.

### Step 3 — Inspect HTTP Headers

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py --headers --url https://www.google.com
```

The `--headers` option requests HTTP header information.

Headers provide information about the server response and HTTP-related configuration.

### Step 4 — Perform WHOIS Lookup

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py --whois --url https://www.google.com
```

The `--whois` option requests domain registration information.

### Step 5 — Perform Web Crawling

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py --crawl --url https://www.google.com
```

The `--crawl` option analyzes the target website and collects accessible links or related page information.

### Step 6 — Explore Full Reconnaissance

Execute:

```bash
python3 /opt/FinalRecon/finalrecon.py --full --url https://www.google.com
```

The `--full` option invokes multiple reconnaissance modules as supported by the installed version.

The complete output and execution behavior depend on the FinalRecon version, available modules, network connectivity, and target responses.

## 5. Command Reference

| Option | Description |
|---|---|
| `-h` | Display help |
| `--sslinfo` | SSL certificate information |
| `--headers` | HTTP header inspection |
| `--whois` | WHOIS lookup |
| `--crawl` | Web crawling |
| `--dns` | DNS enumeration |
| `--sub` | Subdomain enumeration |
| `--dir` | Directory enumeration |
| `--ps` | Port scanning |
| `--full` | Full reconnaissance workflow |
| `--url` | Target URL |

## 6. Technical Interpretation

FinalRecon organizes multiple web reconnaissance features into a command-line interface.

Each module retrieves a different type of information.

Combining certificate inspection, HTTP header analysis, WHOIS information, and crawling can help analysts understand the technology and exposed information associated with a web target.

The results should be interpreted in context and should not automatically be considered proof of a vulnerability.

## 7. Results

The activity explores the help interface, SSL information retrieval, HTTP header inspection, WHOIS lookup, crawling, and full reconnaissance.

The assignment identifies Step 2 as the required screenshot stage.

No specific certificate values or HTTP response headers were preserved in the available activity notes, so no target output is fabricated here.

## 8. Responsible Use

Reconnaissance should be performed only on targets that are publicly available for such testing or where explicit authorization has been obtained.

Directory enumeration and port scanning can generate significant traffic and must remain within the applicable authorization scope.

## 9. Concepts Practiced

- Web reconnaissance
- Open-source intelligence
- SSL/TLS certificate inspection
- HTTP header analysis
- WHOIS information gathering
- Web crawling
- DNS enumeration
- Subdomain discovery
- Automated reconnaissance

## 10. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

Required screenshot: Step 2, showing the SSL information command and its output.

The original assignment places the screenshot instruction immediately before the SSL inspection step, while identifying Step 2 as the required evidence.

## References

- [FinalRecon Official Repository](https://github.com/thewhiteh4t/FinalRecon)
- [Python Documentation](https://docs.python.org/3/)

---

[Back to Class 01](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
