# Activity 4.01 — Modifying Authentication Control Settings on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 13–14  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Change and validate a user's authentication password on Kali Linux, while examining how user and group information is organized in the `/etc/passwd` and `/etc/group` files.

The activity was performed in a controlled academic environment to understand the basic operation of password-based authentication controls in Linux.

## Environment

- **Operating system:** Kali Linux
- **User account:** `aluno`
- **Tools and commands:** `whoami`, `pwd`, `cat`, `sudo`, `passwd`
- **Files examined:** `/etc/passwd` and `/etc/group`

## Procedure

### 1. Identify the Current User and Working Directory

The `whoami` and `pwd` commands were executed:

```bash id="a9f5v2"
whoami
pwd
```

**Observed output:**

```text id="p6j8e4"
┌──(aluno㉿kali)-[~]
└─$ whoami
aluno
                                                                                   
┌──(aluno㉿kali)-[~]
└─$ pwd
/home/aluno
```

The `whoami` command identifies the user associated with the current process.

The `pwd` command (Print Working Directory) displays the full path of the current working directory.

In this case:

- **Current user:** `aluno`
- **Home directory:** `/home/aluno`

### 2. Examine the `/etc/passwd` File

The `/etc/passwd` file was inspected using:

```bash id="q9x2nc"
cat /etc/passwd
```

**Observed output:**

```text id="w3k4mt"
root:x:0:0:root:/root:/usr/bin/zsh
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
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
messagebus:x:100:107::/nonexistent:/usr/sbin/nologin
tcpdump:x:101:109::/nonexistent:/usr/sbin/nologin
sshd:x:102:65534::/run/sshd:/usr/sbin/nologin
polkitd:x:997:997:polkit:/nonexistent:/usr/sbin/nologin
_chrony:x:103:111:Chrony daemon,,,:/var/lib/chrony:/usr/sbin/nologin
kali:x:1000:1001:Kali Linux:/home/kali:/bin/zsh
aluno:x:1001:1002::/home/aluno:/bin/bash
rtkit:x:104:112:RealtimeKit,,,:/proc:/usr/sbin/nologin
usbmux:x:105:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:106:113:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
lightdm:x:107:114:Light Display Manager:/var/lib/lightdm:/bin/false
pulse:x:108:115:PulseAudio daemon,,,:/run/pulse:/usr/sbin/nologin
saned:x:109:118::/var/lib/saned:/usr/sbin/nologin
colord:x:110:119::/var/lib/colord:/usr/sbin/nologin
xrdp:x:111:121::/run/xrdp:/usr/sbin/nologin
Debian-exim:x:112:122::/var/spool/exim4:/usr/sbin/nologin
logcheck:x:113:123:logcheck system account,,,:/var/lib/logcheck:/usr/sbin/nologin
debian-tor:x:114:124::/var/lib/tor:/bin/false
clamav:x:115:125::/var/lib/clamav:/bin/false
geoclue:x:116:126::/var/lib/geoclue:/usr/sbin/nologin
postgres:x:117:130:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
```

The `/etc/passwd` file stores basic information about local user accounts.

Each entry contains seven colon-separated fields:

```text id="n7bc4a"
username:password:UID:GID:GECOS:home:shell
```

Using the `aluno` account as an example:

```text id="mt6w2q"
aluno:x:1001:1002::/home/aluno:/bin/bash
```

The fields are interpreted as follows:

- `aluno` — account name.
- `x` — indicates that the password hash is not stored directly in this file; on modern Linux systems, password hashes are generally stored in `/etc/shadow`.
- `1001` — UID (User ID), the numeric identifier assigned to the user.
- `1002` — GID (Group ID), the numeric identifier of the primary group.
- Empty field — the GECOS/comment field is empty.
- `/home/aluno` — home directory.
- `/bin/bash` — login shell.

The file also contains service accounts that commonly use shells such as `/usr/sbin/nologin` or `/bin/false` to prevent interactive logins.

### 3. Examine the `/etc/group` File

The file containing local group information was inspected using:

```bash id="x8w2fh"
cat /etc/group
```

**Observed output:**

```text id="v6s9kp"
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:kali,logcheck
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:kali
fax:x:21:
voice:x:22:
cdrom:x:24:kali
floppy:x:25:kali
tape:x:26:
sudo:x:27:kali,aluno
audio:x:29:kali,pulse
dip:x:30:kali
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:kali
sasl:x:45:
plugdev:x:46:kali
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:101:
input:x:102:
sgx:x:103:
kvm:x:104:
render:x:105:
netdev:x:106:kali
messagebus:x:107:
_ssh:x:108:
tcpdump:x:109:
polkitd:x:997:
kali-trusted:x:110:
_chrony:x:111:
lxd:x:1000:kali
kali:x:1001:
aluno:x:1002:
rtkit:x:112:
avahi:x:113:
lightdm:x:114:
pulse:x:115:
pulse-access:x:116:
scanner:x:117:saned
saned:x:118:
colord:x:119:
ssl-cert:x:120:aluno,postgres
xrdp:x:121:
Debian-exim:x:122:
logcheck:x:123:
debian-tor:x:124:
clamav:x:125:
geoclue:x:126:
vboxusers:x:127:
docker:x:128:
_cvsadmin:x:129:
postgres:x:130:
```

The entry format is:

```text id="y2x7jn"
group:password:GID:members
```

For example:

```text id="f0m7rw"
sudo:x:27:kali,aluno
```

This indicates that the `sudo` group has GID `27` and lists `kali` and `aluno` as members.

The output shows that `aluno` belongs to the `sudo` group. This membership can permit administrative commands through `sudo`, subject to the system's applicable authorization and authentication configuration.

### 4. Change the User's Password

To change the password for the `aluno` account, administrative access was obtained:

```bash id="px5c8n"
sudo -i
```

The following command was then used:

```bash id="b5z3qn"
passwd aluno
```

The system requested the new password twice and confirmed the change.

**Observed output:**

```text id="t3c7wv"
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:

┌──(root㉿kali)-[~]
└─# passwd aluno
Nova senha:
Redigite a nova senha:
passwd: senha atualizada com sucesso
```

The confirmation message was:

```text id="r9v2fk"
passwd: senha atualizada com sucesso
```

This indicates that the password change completed successfully.

The laboratory password is not reproduced in this README.

### 5. Validate the New Authentication

After changing the password, the user's graphical session was ended.

Kali Linux was then started again, and the new password configured in the previous step was used to authenticate.

The login succeeded, demonstrating that the password change performed with `passwd` had been applied correctly.

### 6. Restore the Original Password

After validating the new credential, the password-change procedure was repeated to restore the original credential used by the laboratory.

The following commands were used:

```bash id="d3hx9v"
sudo -i
passwd aluno
```

After the change was confirmed, the session was ended again.

This step ensured that the laboratory environment remained in the expected state for subsequent activities.

The original and replacement passwords are not documented in this README.

## Commands Used

The following commands were used during the activity:

```bash id="q3gm65"
whoami
pwd
cat /etc/passwd
cat /etc/group
sudo -i
passwd aluno
```

## Concepts Practiced

### `/etc/passwd`

A file that stores basic information about local Linux accounts, including usernames, UIDs, GIDs, home directories, and login shells.

### `/etc/group`

A file that stores information about local groups and their associated members.

### UID and GID

- **UID:** Numeric identifier assigned to a user.
- **GID:** Numeric identifier assigned to a group.

These identifiers help Linux associate processes and file permissions with the appropriate users and groups.

### `/etc/shadow`

Although its contents did not need to be inspected during this activity, `/etc/shadow` is used by Linux to store password hashes and information related to password aging and validity.

Access to this file is restricted because it contains sensitive authentication information.

### `passwd`

A command used to set or change the password of a local account.

### `sudo`

Allows authorized users to execute commands with administrative privileges, subject to the system's configuration.

### Password Authentication

Password-based authentication verifies that a user supplies the credential associated with an account. Changing a password and successfully logging in with the new credential verifies the change from the user's perspective.

## Results

The activity demonstrated the basic operation of password-based authentication controls on Kali Linux.

The following tasks were completed:

- Identified the currently authenticated user.
- Verified the working directory.
- Examined the structure of `/etc/passwd`.
- Examined the structure of `/etc/group`.
- Understood the relationship between users, UIDs, and GIDs.
- Changed a local account password using `passwd`.
- Validated authentication with the new password.
- Restored the laboratory's original password configuration.

The exercise reinforced the importance of proper credential management and access-control mechanisms in Linux systems.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 13–14.

**Recorded screenshot:** Step 7 of the activity, as required by the laboratory instructions, documenting authentication validation after the password change and restoration.

[View Evidence — Classes 13–14](../evidencias.pdf)

---

[Back to Classes 13–14](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
