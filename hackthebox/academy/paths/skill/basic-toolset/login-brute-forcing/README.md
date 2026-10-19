# Login Brute Forcing

> HTB Academy — Basic Toolset

## Overview

Brute-force testing evaluates whether credentials can be guessed through repeated authentication attempts. Practice only against authorized lab targets.

## Key Concepts

- Username and password wordlists
- Authentication protocols and web login forms
- Rate limiting, account lockout, and MFA
- Successful versus failed authentication responses
- Password spraying versus brute-force attacks
- Avoiding account lockouts and unnecessary service load

## Command Reference

| Objective | Example | Notes |
|---|---|---|
| Test SSH credentials with Hydra | `hydra -l <username> -P <wordlist> ssh://<lab-target>` | Authorized lab targets only |
| Review available options | `hydra -h` | Consult help before running a test |

## Practical Workflow

1. Identify the authentication service and permitted scope.
2. Select a relevant test wordlist.
3. Understand lockout and rate-limit protections.
4. Run a controlled test against the lab.
5. Record the result and recommended defensive controls.

## Lab Notes

Add exercise-specific findings and screenshots as you document the Academy labs.

## References

- [THC Hydra](https://github.com/vanhauser-thc/thc-hydra)
