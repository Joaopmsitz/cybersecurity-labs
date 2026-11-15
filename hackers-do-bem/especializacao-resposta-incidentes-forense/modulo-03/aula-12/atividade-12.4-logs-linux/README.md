# Activity 12.4 — Linux Authentication Log and Command History Analysis

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 02  
> **Course Lesson:** 12  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Examine Linux authentication logs and command history to identify evidence of account usage, privilege elevation, and administrative activity.

The activity focuses on the authentication log:

```text
/var/log/auth.log
```

It also examines the root user's command history:

```text
/root/.bash_history
```

The exercise demonstrates how authentication and command history artifacts can be correlated to reconstruct activity on a Linux system.

The activity uses a controlled laboratory environment to demonstrate how an unauthorized account configured with UID 0 and GID 0 can appear in authentication-related records.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux |
| User Account | `aluno` |
| Privilege Level | Root during examination |
| Authentication Log | `/var/log/auth.log` |
| Command History | `/root/.bash_history` |
| Main Commands | `cd`, `ls`, `tail`, `cat`, `su`, `sudo`, `id` |
| Suspicious Account | `user2` |
| Relevant UID | `0` |
| Relevant GID | `0` |

## 3. Linux Log and Authentication Concepts

### Linux System Logs

Linux systems store log information about services, authentication events, kernel activity, and other operating system events.

Many distributions use a logging service such as rsyslog to collect messages and write them to files under:

```text
/var/log
```

Authentication-related records may be stored in:

```text
/var/log/auth.log
```

The exact logging configuration depends on the distribution.

### auth.log

The `auth.log` file commonly contains messages related to authentication and authorization.

Examples include:

- Login and authentication attempts.
- PAM session events.
- `sudo` activity.
- `su` account switching.
- Session opening and closing events.

These events can help reconstruct privilege changes and account usage.

### PAM and Session Records

PAM (Pluggable Authentication Modules) provides a mechanism for applications to authenticate users and manage sessions.

Log messages containing:

```text
pam_unix
```

can indicate authentication or session events handled by the Unix PAM module.

### Shell History

Bash can maintain a command history for each user.

The history file is commonly named:

```text
.bash_history
```

For the root account, the file is normally located at:

```text
/root/.bash_history
```

The file may contain commands entered during earlier shell sessions.

It can provide valuable investigative context, although it is not a complete or tamper-proof audit trail.

## 4. Procedure

### Step 1 — Inspect the Linux Log Directory

The first step was to access the log directory:

```bash
cd /var/log
```

The directory contents were listed:

```bash
ls -la
```

The supplied course output begins as follows:

```text
total 2516

drwxr-xr-x  9 root root       4096 Jun 11 00:00 .
drwxr-xr-x 12 root root       4096 Jun 10 15:31 ..
-rw-r--r--  1 root root          0 Jun  4 12:57 alternati
-rw-r--r--  1 root root       3590 May 30 12:56 alternati
drwxr-x---  2 root adm        4096 Jun 13 00:00 apache2
drwxr-xr-x  2 root root       4096 Jun 10 15:31 apt
-rw-r-----  1 root adm       32030 Jun 13 01:25 auth.log
-rw-r-----  1 root adm       91103 Jun 10 23:17 auth.log
-rw-r-----  1 root adm        4392 May 30 15:17 auth.log
-rw-rw----  1 root utmp       384 Jun  5 11:24 btmp
-rw-rw----  1 root utmp       384 May 30 13:21 btmp.1
drwxr-x---  2 _chrony _chrony 4096 May 29 21:42 chrony
-rw-r-----  1 root adm       92765 Jun 13 00:00 daemon.lo
-rw-r-----  1 root adm      353374 Jun 11 00:00 daemon.lo
-rw-r-----  1 root adm       10587 Jun  4 12:57 daemon.lo
-rw-r-----  1 root adm        8155 Jun 12 22:50 debug
-rw-r-----  1 root adm       19200 Jun  4 23:24 debug.1
-rw-r-----  1 root adm        1019 May 29 21:49 debug.2.g
-rw-r--r--  1 root root      22742 Jun 10 15:31 dpkg.log
-rw-r--r--  1 root root     123199 May 30 13:08 dpkg.log
-rw-r--r--  1 root root      32064 Jun  5 11:20 faillog
-rw-r--r--  1 root root        484 May 30 12:55 fontconfi
drwxr-sr-x+ 3 root systemd-journal 4096 May 29 21:42 journal
-rw-r-----  1 root adm      116946 Jun 12 22:50 kern.log
-rw-r-----  1 root adm      249629 Jun 10 21:07 kern.log
-rw-r-----  1 root adm       13187 Jun  4 12:57 kern.log
-rw-rw-r--  1 root utmp    292584 Jun 12 22:50 lastlog
-rw-r-----  1 root adm      108165 Jun 12 22:50 messages
-rw-r-----  1 root adm      233452 Jun 10 21:07 messages
-rw-r-----  1 root adm       12952 Jun  4 12:57 messages
drwx------  2 root root       4096 May 29 21:42 private
drwxr-xr-x  3 root root       4096 May  1 19:30 runit
-rw-r-----  1 root adm      213274 Jun 13 01:17 syslog
-rw-r-----  1 root adm      612069 Jun 11 00:00 syslog.1
-rw-r-----  1 root adm       24652 Jun  4 12:57 syslog.2
drwxr-x---  2 root adm        4096 Jun  4 12:57 unattende
-rw-r-----  1 root adm        1640 Jun 12 22:50 user.log
-rw-r-----  1 root adm        4738 Jun  4 23:24 user.log
-rw-r-----  1 root adm         513 May 30 12:57 user.log
-rw-------  1 root root       1295 May 29 21:44 vboxadd-i
-rw-r--r--  1 root root        155 May 30 12:12 vboxadd-s
-rw-r--r--  1 root root        216 May 29 21:49 vboxadd-s
-rw-r--r--  1 root root        216 May 29 21:44 vboxadd-s
-rw-r--r--  1 root root        358 May 29 21:44 vboxadd-s
-rw-rw-r--  1 root utmp     31488 Jun 12 22:50 wtmp
```

The output shows several system log files.

The relevant file for this activity is:

```text
auth.log
```

The directory also contains other logs such as `syslog`, `kern.log`, `daemon.log`, `lastlog`, and `wtmp`.

### Step 2 — Examine the Authentication Log

The activity then examined `auth.log` using:

```bash
tail auth.log
```

The supplied output excerpt is:

```text
Jun 13 00:17:01 forense-linux CRON[1586]: pam_unix(cron:session): se...
Jun 13 00:17:01 forense-linux CRON[1586]: pam_unix(cron:session): se...
Jun 13 01:17:01 forense-linux CRON[1592]: pam_unix(cron:session): se...
Jun 13 01:17:01 forense-linux CRON[1592]: pam_unix(cron:session): se...
Jun 13 01:25:48 forense-linux sudo: aluno : TTY=pts/0 ; PWD=/var/lo...
Jun 13 01:25:48 forense-linux sudo: pam_unix(sudo:session): session ...
Jun 13 01:25:48 forense-linux sudo: pam_unix(sudo:session): session ...
Jun 13 01:36:03 forense-linux sudo: aluno : TTY=pts/0 ; PWD=/var/lo...
```

Some lines in the supplied course extraction are clipped.

The records show activity from CRON and `sudo`, including PAM session events.

The timestamps and process identifiers provide context for correlating system activity.

### Step 3 — Examine the Added Account in the Laboratory

The course then demonstrates how an account with root-equivalent identifiers can be introduced into the active laboratory system.

The prepared `user2` record from Activity 12.3 was used for this demonstration.

The corresponding account information was inspected in:

```bash
cat /etc/passwd
```

The supplied output contains the following relevant records:

```text
root:x:0:0:root:/root:/bin/bash
...
aluno:x:1000:1000::/home/aluno:/bin/bash
...
user2:/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bash
```

The displayed output reflects the terminal text provided by the course material.

The original `echo` command in the handout is clipped in the extracted text and contains `$` characters inside double quotes. Those characters are interpreted by Bash as parameter expansions unless escaped or quoted literally.

For that reason, the incomplete command is not reproduced as a ready-to-run account-modification instruction in this forensic report.

The relevant observation is the resulting account record and its UID and GID values.

### Step 4 — Switch to the Suspicious Account and Check Its Identity

The account was accessed from the root shell:

```bash
su user2
```

The account identity was then inspected:

```bash
id
```

The terminal returned:

```text
uid=0(root) gid=0(root) groups=0(root)
```

This output confirms that the session associated with `user2` has UID 0 and GID 0.

The account therefore has root-equivalent identity values.

This is a significant finding because an account with those identifiers can receive the same user and group-level permission treatment as root.

### Step 5 — Review Authentication Logs After the Account Switch

The shell was returned to the root context:

```bash
sudo su
```

The authentication log was examined again:

```bash
tail auth.log
```

The output provided by the course includes:

```text
Jun 13 01:47:58 forense-linux sudo: pam_unix(sudo:session): session ...
Jun 13 01:47:58 forense-linux su: (to root) aluno on pts/0
Jun 13 01:47:58 forense-linux su: pam_unix(su:session): session open...
Jun 13 01:51:20 forense-linux su: (to user2) aluno on pts/0
Jun 13 01:51:20 forense-linux su: pam_unix(su:session): session open...
Jun 13 01:53:35 forense-linux sudo: aluno : TTY=pts/0 ; PWD=/var/lo...
Jun 13 01:53:35 forense-linux sudo: pam_unix(sudo:session): session ...
```

The records show session activity associated with switching to root and then to `user2`.

The `su` records are important because they provide evidence of account switching.

The `sudo` and PAM session messages provide additional context about privilege-related activity.

### Step 6 — Examine the Root User's Command History

The course then examines the command history maintained for the root account.

The root user's home directory was accessed:

```bash
cd /root
```

The history file was displayed:

```bash
cat .bash_history
```

The supplied output contains the following commands:

```text
sudo apt install openssl
git clone "https://github.com/magnumripper/JohnTheRipper.git" && cd...
apt install install libssl-dev libssl1.0.0=1.0.1e-2+deb7u14
apt install install libs
apt install libssl-dev libssl1.0.0=1.0.1e-2+deb7u14
apt install libssl-dev
./configure && sudo make -s clean && sudo make -sj4
exit
cat /etc/shadow
cat /etc/shadow > shadow
cat /etc/passwd > passwd
exit
history | grep volatility
exit
echo "user2:$1$user2$hgMHLsJ/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bas...
cat /etc/passwd
exit
```

Some command lines are truncated in the supplied course extraction.

The history provides evidence of commands associated with:

- Installing OpenSSL and development libraries.
- Cloning the John the Ripper repository.
- Compiling software.
- Reading and copying `/etc/shadow`.
- Reading and copying `/etc/passwd`.
- Searching command history for Volatility-related activity.
- The `user2` account modification demonstration.

The history file provides an additional source of investigative information.

## 5. Expected Results

The activity demonstrates how Linux logs and shell history can provide evidence of account and privilege-related activity.

The relevant findings are:

| Artifact | Finding |
|---|---|
| `/var/log/auth.log` | Contains CRON, sudo, PAM, and su session records |
| `/etc/passwd` | Contains the `user2` account entry used in the laboratory demonstration |
| `id` output | Reports `uid=0(root) gid=0(root) groups=0(root)` |
| `su` log records | Show session switching to `root` and `user2` |
| `/root/.bash_history` | Contains commands related to account files, software compilation, and forensic tools |

The combined information demonstrates how multiple system artifacts can support the reconstruction of activity.

## 6. Technical Analysis

### Authentication Log Interpretation

The `auth.log` file contains authentication-related records.

The initial output includes:

```text
sudo
pam_unix
CRON
```

These records are useful when reconstructing account and session activity.

The later output contains:

```text
su: (to root) aluno on pts/0
su: (to user2) aluno on pts/0
```

These records indicate account-switching activity from the `aluno` session.

### Why the id Command Matters

The command:

```bash
id
```

displays the effective user and group identifiers for the current session.

The result:

```text
uid=0(root) gid=0(root) groups=0(root)
```

shows that the `user2` session has root-equivalent UID and GID values.

This provides direct confirmation of the identity associated with the session, rather than relying only on the account's name.

### Authentication Logs and Command History Are Different Sources

Authentication logs and shell history provide complementary information.

| Artifact | Type of Information |
|---|---|
| `auth.log` | Authentication, session, PAM, sudo, and su events |
| `.bash_history` | Commands entered in Bash sessions |

An authentication log can indicate that a session was opened or that an account switch occurred.

A shell history file can provide context about commands entered by the user.

Neither source is necessarily complete or tamper-proof.

For example, Bash history can be cleared, disabled, or modified. Authentication records can also be rotated, deleted, or altered by an attacker with sufficient privileges.

### Interpreting the Root Command History

The root user's history contains commands that reference:

```text
/etc/shadow
/etc/passwd
JohnTheRipper
Volatility
```

These commands may be relevant to an investigation because they indicate access to account databases and the installation or compilation of tools.

The presence of a command in shell history is not equivalent to proof that it completed successfully.

The history should be correlated with filesystem timestamps, authentication records, process artifacts, and other logs.

### Forensic Collection in a Live Environment

The course uses a running Linux machine to demonstrate log examination.

In a real forensic investigation, the examiner would normally collect and preserve the relevant artifacts as part of a documented evidence acquisition process.

Live-system examination can alter system state and should be recorded as part of the forensic procedure.

## 7. Results and Interpretation

The activity demonstrates the analysis of Linux authentication logs and shell history.

The initial examination of `/var/log/auth.log` identified records related to CRON and sudo sessions.

The `user2` account was then tested in the laboratory.

The `id` command returned:

```text
uid=0(root) gid=0(root) groups=0(root)
```

The subsequent `auth.log` examination showed account-switching records involving root and `user2`.

Finally, `/root/.bash_history` provided additional context about commands associated with password files, software installation, compilation, and forensic tools.

The results demonstrate why authentication logs and command history should be analyzed together during a Linux forensic investigation.

## 8. Concepts Practiced

- Linux log analysis
- `/var/log`
- `auth.log`
- `ls -la`
- `tail`
- Authentication records
- PAM session events
- sudo activity
- su account switching
- UID and GID
- Root-equivalent accounts
- `id`
- Bash command history
- `/root/.bash_history`
- Account database examination
- Evidence correlation
- Live-system forensic analysis

## 9. Evidence

**Required screenshot: Print 4 — PDF page 4 — Step 6.**

The assignment explicitly requires the screenshot for Step 6.

Step 6 is the examination of the root user's command history:

```bash
cd /root
cat .bash_history
```

The screenshot should show the command and its resulting output under the personalized terminal prompt.

**Evidence discrepancy to verify:** the supplied description of Print 4 mentions `tail auth.log`, which appears in Steps 2 and 5. The assignment instructions specifically request Step 6, which is the `.bash_history` output. Confirm that page 4 of the PDF contains the Step 6 evidence; otherwise, the submitted print may not satisfy the stated requirement.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 12.4 is on page 4 of the consolidated PDF.

## References

- [Debian Handbook — System Logs](https://www.debian.org/doc/manuals/debian-handbook/sect.syslog.en.html)
- [Linux Manual — passwd(5)](https://man7.org/linux/man-pages/man5/passwd.5.html)
- [GNU Bash — History Facilities](https://www.gnu.org/software/bash/manual/html_node/Bash-History-Facilities.html)
- [Linux Manual — su(1)](https://man7.org/linux/man-pages/man1/su.1.html)
- [Linux Manual — sudo(8)](https://man7.org/linux/man-pages/man8/sudo.8.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 12.5](../atividade-12.5-alternate-data-streams/README.md)
