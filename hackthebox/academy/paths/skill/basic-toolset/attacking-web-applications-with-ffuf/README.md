# <img src="./images/attacking-web-applications-with-ffuf.jpg" width="36" alt="Attacking Web Applications with Ffuf"> Attacking Web Applications with Ffuf

> HTB Academy — Basic Toolset

## Overview

Ffuf is a web fuzzer used to discover resources and test input locations in authorized web assessments.

## Command Reference

| Objective | Example | Notes |
|---|---|---|
| Discover directories | `ffuf -w wordlist.txt -u http://<lab-target>/FUZZ` | FUZZ is replaced by each word |
| Test file extensions | `ffuf -w wordlist.txt -u http://<lab-target>/FUZZ -e .php,.txt` | Adjust extensions to the lab |
| Discover virtual hosts | `ffuf -w subdomains.txt -u http://<lab-target>/ -H "Host: FUZZ.example.local"` | Use the authorized hostname scope |
| Filter status codes | `ffuf -w wordlist.txt -u http://<lab-target>/FUZZ -fc 404` | Hides responses with the selected code |
| Save results | `ffuf -w wordlist.txt -u http://<lab-target>/FUZZ -o results.json -of json` | Saves JSON output |

## Key Concepts

- Directory and file discovery
- Virtual-host fuzzing
- Parameter discovery
- Wordlist selection
- Response codes, sizes, words, and filtering
- Interpreting false positives

## Practical Workflow

1. Confirm the permitted target and wordlist.
2. Identify the correct FUZZ position.
3. Run a controlled discovery pass.
4. Filter unhelpful responses.
5. Validate interesting results manually.

## Lab Notes

Add exercise-specific payloads, findings, and screenshots as you document the Academy labs. Store screenshots in `images/` and detailed write-ups in a `labs/` directory.

## References

- [Ffuf project](https://github.com/ffuf/ffuf)

## Completion

<a href="https://academy.hackthebox.com/achievement/badge/00a6ff26-cca4-11f0-9254-bea50ffe6cb4"><img src="./images/htb-attacking-web-applications-with-ffuf-badge.png" width="120" alt="HTB Academy — Fuzzing is power Badge"></a>

**Completed:** 28 November 2025
