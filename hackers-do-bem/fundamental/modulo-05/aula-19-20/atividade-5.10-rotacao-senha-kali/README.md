# Activity 5.10 — Password Rotation on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 19–20  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity demonstrates how to configure password aging policy on Kali Linux.

The exercise uses `passwd -S` to inspect information about user passwords and then modifies `/etc/login.defs` to configure password validity, the minimum interval between password changes, and the warning period before expiration.

The exercise illustrates how password policy parameters can be configured directly in a Linux system.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`

The credentials used in the laboratory are not recorded in this README.

## Procedure

### 1. Open the Terminal

After accessing the Kali Linux machine through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

Administrative access was required because the activity involved inspecting and modifying system configuration settings.

### 2. Inspect the Root User's Password Policy

With administrative privileges, the following command was executed:

```bash
passwd -S
```

**Observed output:**

```text
┌──(root㉿kali)-[~]
└─# passwd -S
root P 2024-07-02 0 99999 7 -1
```

The `passwd -S` command displays a summary of the user's password status.

The output:

```text
root P 2024-07-02 0 99999 7 -1
```

can be interpreted as follows:

| Field | Value | Meaning |
|---|---|---|
| User | `root` | Account being inspected |
| Status | `P` | Password is set |
| Last change | `2024-07-02` | Date of the last password change |
| Minimum | `0` | Minimum number of days before another password change is permitted |
| Maximum | `99999` | Maximum password validity period in days |
| Warning | `7` | Number of days before expiration when a warning begins |
| Inactive | `-1` | Password inactivity period is disabled |

These values represent the policy information reported for the account at the time of the query.

### 3. Inspect the `aluno` User's Password Policy

After checking the root account, the administrative session was ended:

```bash
exit
```

The following command was then executed again:

```bash
passwd -S
```

**Observed output:**

```text
┌──(aluno㉿kali)-[~]
└─$ passwd -S
aluno P 2025-09-06 0 99999 7 -1
```

The output has the same structure but refers to the `aluno` user:

```text
aluno P 2025-09-06 0 99999 7 -1
```

The main values observed were:

- **User:** `aluno`
- **Password status:** `P`
- **Last recorded change:** `2025-09-06`
- **Minimum interval:** 0 days
- **Maximum validity period:** 99,999 days
- **Expiration warning:** 7 days
- **Inactivity period after expiration:** Disabled (`-1`)

The date shown corresponds to the output recorded in the laboratory material and may vary depending on the machine used.

### 4. Edit the Configuration File

To configure the password policy parameters, the `nano` editor was used with administrative privileges:

```bash
sudo nano /etc/login.defs
```

The `/etc/login.defs` file contains configuration settings used by tools related to account and password management on Linux systems.

The following parameters were located in the file:

```text
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
```

These values represent the previous configuration observed in the laboratory.

### 5. Configure Password Aging

The parameters were changed to the following values:

```text
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

These values establish the following settings.

#### PASS_MAX_DAYS

```text
PASS_MAX_DAYS   270
```

Defines the maximum number of days a password may remain valid before a change is required.

In this laboratory, the configured maximum validity period was 270 days.

#### PASS_MIN_DAYS

```text
PASS_MIN_DAYS   90
```

Defines the minimum number of days that must elapse before the user is permitted to change the password again.

In this laboratory, the minimum interval was set to 90 days.

#### PASS_WARN_AGE

```text
PASS_WARN_AGE   10
```

Defines how many days in advance the system should warn the user that the password is approaching expiration.

In this laboratory, the warning period was set to 10 days before expiration.

### 6. Save the Configuration

After modifying `/etc/login.defs`, the file was saved in `nano` using:

```text
Ctrl + X
S
Enter
```

The terminal was then closed.

## Concepts Practiced

### Password Rotation

Password rotation involves establishing rules that determine when a password must be changed.

In corporate environments, such policies may form part of identity and access management controls by defining administrative requirements for credentials.

Password expiration policies should be aligned with the organization's security requirements. Periodic password changes are not a substitute for strong passwords, multifactor authentication, monitoring, or changing credentials when compromise is suspected.

### `/etc/login.defs`

The file:

```text
/etc/login.defs
```

stores various parameters related to Linux account management.

The following parameters were used in this activity:

```text
PASS_MAX_DAYS
PASS_MIN_DAYS
PASS_WARN_AGE
```

**Technical note:** These settings generally define default password-aging values used by account-management tools when creating accounts. Editing `/etc/login.defs` does not necessarily change the existing password-aging values of users who are already configured. Existing account settings can be inspected and managed separately with tools such as `chage`.

### Configured Policy

The final configuration entered in the laboratory was:

```text
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

It can be represented as follows:

```text
Password
 │
 ├── Maximum validity: 270 days
 │
 ├── Minimum interval between changes: 90 days
 │
 └── Expiration warning: 10 days
```

## Results

The activity demonstrated how to inspect password-aging information using `passwd -S` and configure new default values in `/etc/login.defs`.

The previous configuration observed in the laboratory was:

```text
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
```

After editing the file, the configured values were:

```text
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

This established the intended default password-aging policy for a maximum validity period of 270 days, a minimum interval of 90 days between changes, and an expiration warning 10 days in advance.

The configuration file was updated during the activity. The recorded procedure did not include a subsequent verification showing that the new values had been applied to the existing `root` and `aluno` accounts.

## Evidence

The evidence for this activity corresponds to Step 5, showing the configured parameters in `/etc/login.defs`:

```text
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

[View Evidence — Classes 19–20](../evidencias.pdf)

---

[Back to Classes 19–20](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
