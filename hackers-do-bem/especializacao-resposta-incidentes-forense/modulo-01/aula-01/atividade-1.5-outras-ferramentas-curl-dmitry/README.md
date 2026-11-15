# Activity 1.5 — Information Gathering with cURL and DMitry

> **Program:** Hackers do Bem
> **Stage:** Specialization — Incident Response and Digital Forensics
> **Module:** 01
> **Class:** 01
> **Environment:** forenseLinux VM
> **Status:** Completed

## 1. Objective

Explore additional reconnaissance tools for gathering information about network addresses and domain names.

The activity uses cURL with IPinfo to retrieve IP intelligence and DMitry to gather domain and network information.

## 2. Environment

| Item | Details |
|---|---|
| Operating System | forenseLinux |
| Tools | cURL, DMitry |
| Information Service | IPinfo |
| Example IP | 45.33.32.156 |
| Example Domain | google.com |
| Output File | dmitry.txt |

## 3. Part A — IP Intelligence with cURL

cURL is a command-line tool used to transfer data through supported protocols.

The exercise uses it to retrieve information from the IPinfo service.

### Step 1 — Query IPinfo

Execute:

```bash
curl ipinfo.io/45.33.32.156
```

Example JSON output provided by the training material:

```json
{
  "ip": "45.33.32.156",
  "hostname": "scanme.nmap.org",
  "city": "Fremont",
  "region": "California",
  "country": "US",
  "loc": "37.5483,-121.9886",
  "org": "AS63949 Akamai Connected Cloud",
  "postal": "94536",
  "timezone": "America/Los_Angeles",
  "readme": "https://ipinfo.io/missingauth"
}
```

### Output Interpretation

| Field | Meaning |
|---|---|
| `ip` | Queried IP address |
| `hostname` | Associated hostname, when available |
| `city` | City associated with the IP registration data |
| `region` | Administrative region |
| `country` | Country code |
| `loc` | Approximate coordinates |
| `org` | Network organization or ASN description |
| `postal` | Postal code associated with the IP information |
| `timezone` | Time zone associated with the location |
| `readme` | Additional service information |

The output above is the historical example supplied in the assignment. Geolocation and network ownership data can change and should be queried again when performing a current investigation.

The `loc` field should not be interpreted as the precise physical location of a device or user.

## 4. Part B — Domain Reconnaissance with DMitry

DMitry stands for Deepmagic Information Gathering Tool.

It is a Linux command-line reconnaissance application capable of gathering different types of information about a target host.

The exercise introduces the following capabilities:

- Domain WHOIS.
- IP WHOIS.
- Subdomain enumeration.
- Email address discovery.
- TCP port scanning.
- Output collection.

### Step 2 — Execute DMitry

The original assignment provides:

```bash
/bin/dmitry google.com
```

The training material shows a partial example output:

```text
HostIP:216.58.203.206
HostName:google.com
[...]
```

The actual output depends on the target, DNS records, available external services, and the DMitry version.

### Step 3 — Save Results to a Text File

Execute:

```bash
dmitry -wise -o dmitry.txt google.com
```

The command saves the collected information to:

```text
/home/aluno/dmitry.txt
```

The relevant command options are:

| Option | Function |
|---|---|
| `-w` | WHOIS lookup for a domain |
| `-i` | WHOIS lookup for an IP address |
| `-s` | Search for possible subdomains |
| `-e` | Search for possible email addresses |
| `-p` | Perform a TCP port scan |
| `-o` | Save results to a specified output file |

The activity command uses:

```text
-wise
```

It therefore enables the domain WHOIS, IP WHOIS, subdomain search, and email search options.

It does not include `-p`, so the saved-output command does not explicitly request the TCP port scanning module.

### Inspect the Generated File

The generated file can be inspected using:

```bash
cat dmitry.txt
```

Alternatively:

```bash
less dmitry.txt
```

The original assignment requires a screenshot of the file contents.

## 5. Technical Interpretation

cURL and DMitry provide complementary reconnaissance capabilities.

cURL retrieves data from IPinfo through an HTTP request.

DMitry consolidates several reconnaissance techniques into one command-line application.

Saving the DMitry results to a text file provides a persistent record that can be reviewed and used during subsequent analysis.

IP intelligence and registration data should be treated as contextual information rather than proof of the exact location or identity of a system.

## 6. Results

The activity demonstrates two information-gathering approaches:

1. Retrieving IP-related information through cURL and IPinfo.
2. Gathering domain information through DMitry and saving the output.

The IPinfo JSON and partial DMitry output included above are examples preserved from the training material.

The actual generated `dmitry.txt` contents were not included in the written activity notes.

## 7. Concepts Practiced

- cURL
- HTTP requests
- JSON response interpretation
- IP intelligence
- ASN and organization information
- WHOIS
- Subdomain enumeration
- Email reconnaissance
- TCP scanning options
- Command output preservation
- Technical documentation

## 8. Evidence

[View Universal Class Evidence PDF](../evidences.pdf)

Required screenshot: Step 3, showing the `dmitry.txt` output.

## References

- [IPinfo](https://ipinfo.io/)
- [Kali Linux — DMitry](https://www.kali.org/tools/dmitry/)
- [Debian DMitry Manual](https://manpages.debian.org/testing/dmitry/dmitry.1.en.html)
- [cURL Documentation](https://curl.se/docs/)

---

[Back to Class 01](../README.md) · [Back to Module 01](../../README.md) · [Back to Specialization](../../../README.md)
