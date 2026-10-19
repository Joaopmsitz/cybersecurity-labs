# <img src="./images/javascript-deobfuscation.jpg" width="36" alt="JavaScript Deobfuscation"> JavaScript Deobfuscation

> HTB Academy — Cracking into Hack the Box

## Overview

JavaScript deobfuscation helps analysts understand code whose structure or values have been deliberately obscured. It is useful when reviewing unfamiliar web scripts or suspicious client-side code.

## Core Concepts

- Source inspection and external JavaScript files
- Beautification of compressed code
- Base64, hexadecimal, URL encoding, and character-code conversions
- String arrays and dynamic property access
- Static analysis without executing the script
- Tracing browser behavior and network requests

## Command Reference

| Objective | Example | Purpose |
|---|---|---|
| Download a script | `curl -s https://<lab-target>/script.js -o script.js` | Saves a local copy |
| Beautify JavaScript | `js-beautify script.js -o script.pretty.js` | Improves readability when installed |
| Locate decoding patterns | `grep -nE 'eval|atob|fromCharCode|unescape|decodeURIComponent' script.pretty.js` | Highlights areas for review |
| Inspect source safely | `less script.pretty.js` | Supports manual static analysis |

Treat unfamiliar scripts as untrusted. Avoid executing suspicious code on your normal workstation.

## Practical Workflow

1. Locate the relevant JavaScript.
2. Save a copy for analysis.
3. Beautify or reformat the source.
4. Identify encoded values and decoding logic.
5. Decode values in a controlled manner.
6. Trace relevant functions and network requests.
7. Document evidence and conclusions.

## Lab Notes

Add exercise-specific examples, findings, and screenshots as you document the Academy labs.

## Completion

<a href="https://academy.hackthebox.com/achievement/badge/74fa947a-cfb3-11f0-9254-bea50ffe6cb4"><img src="./images/htb-javascript-deobfuscation-badge.png" width="120" alt="HTB Academy — Playing with the mess Badge"></a>

**Completed:** 2 December 2025

## References

- [HTB Academy — JavaScript Deobfuscation](https://academy.hackthebox.com/app/module/41)
- [MDN — JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
