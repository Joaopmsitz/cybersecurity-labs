# <img src="./images/sqlmap-essentials.jpg" width="36" alt="SQLMap Essentials"> SQLMap Essentials

> HTB Academy — Basic Toolset

## Overview

SQLMap automates the detection and assessment of SQL injection vulnerabilities in authorized test environments.

## Command Reference

| Objective | Example | Notes |
|---|---|---|
| Test a URL parameter | `sqlmap -u "http://<lab-target>/item.php?id=1" -p id` | Restricts testing to the specified parameter |
| Use non-interactive defaults | `sqlmap -u "http://<lab-target>/item.php?id=1" -p id --batch` | Accepts default prompts |
| Review database names | `sqlmap -u "<authorized-lab-url>" --dbs` | Use only within the allowed lab scope |
| List tables | `sqlmap -u "<authorized-lab-url>" -D <database> --tables` | Requires a confirmed test context |
| Inspect columns | `sqlmap -u "<authorized-lab-url>" -D <database> -T <table> --columns` | Helps characterize the test database |

## Key Concepts

- SQL injection detection
- GET and POST parameters
- Cookies and authenticated requests
- Database types and enumeration
- Request files and reproducible tests
- Impact assessment and remediation

## Practical Workflow

1. Confirm the authorized test URL.
2. Identify parameters and request context.
3. Test a narrow parameter scope.
4. Evaluate the evidence returned by SQLMap.
5. Document impact and remediation, such as parameterized queries.

## Lab Notes

Record the vulnerable parameter, evidence, database behavior, and the relevant exercise findings. Do not test or extract data from systems outside the authorized lab.

## References

- [SQLMap project and documentation](https://github.com/sqlmapproject/sqlmap)
