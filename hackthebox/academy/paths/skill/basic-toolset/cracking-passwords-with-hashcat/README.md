# Cracking Passwords with Hashcat

> HTB Academy — Basic Toolset

## Overview

Hashcat performs password-recovery tests against password hashes. Use it only with hashes you own or are explicitly authorized to assess.

## Command Reference

| Objective | Example | Notes |
|---|---|---|
| Dictionary attack | `hashcat -m <mode> hashes.txt wordlist.txt` | Select the mode for the actual hash type |
| Apply a rule | `hashcat -m <mode> hashes.txt wordlist.txt -r rules/best64.rule` | Transforms candidate passwords |
| Mask attack | `hashcat -m <mode> -a 3 hashes.txt <mask>` | Tests candidates matching a mask |
| Show recovered results | `hashcat -m <mode> hashes.txt --show` | Displays recovered passwords |
| View example hash formats | `hashcat --example-hashes` | Helps review supported formats |

## Key Concepts

- Hash types and mode selection
- Wordlists and candidate generation
- Rule-based mutations
- Mask attacks and keyspaces
- Hardware performance and workload
- Salting and secure password storage

## Practical Workflow

1. Confirm the hash format.
2. Choose an appropriate attack mode.
3. Select a wordlist, rule, or mask.
4. Run the authorized recovery task.
5. Save and review results without exposing unrelated credentials.

## Lab Notes

Record the hash type, chosen mode, attack strategy, and lab outcome.

## References

- [Hashcat documentation](https://hashcat.net/wiki/)
- [Hashcat project](https://github.com/hashcat/hashcat)
