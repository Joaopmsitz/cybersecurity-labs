# Activity 5.09 — Role-Based Access Control (RBAC) on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 05  
> **Class:** 19–20  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity demonstrates access control concepts related to Role-Based Access Control (RBAC) on Kali Linux.

The exercise involves creating a group representing a specific function, adding a user to that group, and assigning the group as the group owner of a file used in the activity. This allows access to the resource to be managed through the user's membership in the group associated with the function.

**Technical note:** The exercise uses traditional Linux groups and file permissions to illustrate a role-based access concept. This is not, by itself, a complete RBAC implementation.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Working directory:** `/home/aluno/Documentos/`

The credentials used in the laboratory are not recorded in this document.

## Procedure

### 1. Open the Terminal

After accessing the Kali Linux machine through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

The directory used in the activity was then accessed:

```bash
cd /home/aluno/Documentos/
```

### 2. Verify the Existing File

The `ls` command was used to inspect the files in the directory:

```bash
ls
```

**Observed output:**

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls
texto.txt
```

The `texto.txt` file was created in the previous activity and was used here to demonstrate assigning permissions through a group.

### 3. List the System Users

To view the users available on the system, the following command was executed:

```bash
getent passwd | cut -d: -f1
```

**Observed output:**

```text
root
daemon
bin
sys
sync
games
man
lp
mail
news
uucp
proxy
www-data
backup
list
irc
_apt
nobody
systemd-network
messagebus
tcpdump
sshd
polkitd
_chrony
kali
systemd-timesync
aluno
rtkit
xrdp
usbmux
avahi
pulse
saned
lightdm
colord
tss
dnsmasq
strongswan
speech-dispatcher
nm-openvpn
nm-openconnect
postgres
Debian-exim
logcheck
debian-tor
freerad
clamav
geoclue
_rpc
pipewire
statd
teste1
```

The command combines two operations:

```bash
getent passwd
```

This retrieves user entries from the databases configured on the system.

The following command:

```bash
cut -d: -f1
```

splits each entry using `:` as the delimiter and displays only the first field, which corresponds to the username.

### 4. List the System Groups

To view the existing groups, the following command was executed:

```bash
getent group | cut -d: -f1
```

**Observed output:**

```text
root
daemon
bin
sys
adm
tty
disk
lp
mail
news
uucp
man
proxy
kmem
dialout
fax
voice
cdrom
floppy
tape
sudo
audio
dip
www-data
backup
operator
list
irc
src
shadow
utmp
video
sasl
plugdev
staff
games
users
nogroup
systemd-journal
systemd-network
crontab
input
sgx
kvm
render
netdev
messagebus
tcpdump
_ssh
polkitd
kali-trusted
_chrony
lxd
kali
systemd-timesync
aluno
rtkit
ssl-cert
xrdp
avahi
pulse
pulse-access
scanner
saned
lightdm
colord
tss
bluetooth
plocate
nm-openvpn
pipewire
nm-openconnect
postgres
wireshark
Debian-exim
logcheck
debian-tor
freerad
clamav
geoclue
docker
_cvsadmin
vboxusers
clock
teste1
```

As in the previous command, `getent group` retrieves group information, while `cut -d: -f1` displays only each group's name.

### 5. Create the Functional Group

To represent a specific function within the environment, the following group was created:

```bash
groupadd contabilidade
```

The `groupadd` command creates a new group on the system.

In this laboratory, the group was named:

```text
contabilidade
```

Groups can be used to organize users according to a particular function or responsibility.

### 6. Confirm Group Creation

After creating the group, the group listing was executed again:

```bash
getent group | cut -d: -f1
```

At the end of the output, the following group was visible:

```text
contabilidade
```

This confirms that the new group was created on the system.

### 7. Add the User to the Group

The `teste1` user was added to the `contabilidade` group using:

```bash
usermod -aG contabilidade teste1
```

The command consists of the following elements:

- `usermod` — modifies a user account.
- `-a` — appends the new group membership without removing existing supplementary group memberships.
- `-G` — specifies supplementary groups.
- `contabilidade` — the group to which the user will be added.
- `teste1` — the user receiving the group membership.

Using `-aG` is important because it adds the user to the new group while preserving other supplementary group memberships.

### 8. Assign the Group to the File

After creating the group and adding the user, the `contabilidade` group was assigned to `texto.txt`:

```bash
chown :contabilidade texto.txt
```

The `chown` command changes the owner and/or group associated with a file.

In this case, the syntax:

```bash
chown :contabilidade texto.txt
```

indicates that only the file's group ownership is being changed, while the existing owner is retained.

The file is therefore associated with the following group:

```text
contabilidade
```

### 9. Change the File Permissions

To complete the access configuration, the following command was executed:

```bash
chmod 770 texto.txt
```

The `770` permission can be represented as follows:

```text
7    7    0
│    │    │
│    │    └── others
│    └─────── group
└──────────── owner
```

Each number is formed by combining permission values:

```text
4 = read    (r)
2 = write   (w)
1 = execute (x)
```

Therefore:

```text
7 = 4 + 2 + 1 = rwx
```

With mode `770`, the resulting permissions are:

```text
owner  → rwx
group  → rwx
others → ---
```

This means:

- The owner has read, write, and execute permissions.
- Members of the group have read, write, and execute permissions.
- Other users have no permissions on the file.

This configuration allows the group to be used as a mechanism for controlling access to the resource.

**Technical note:** For a text file, the execute bit grants execution permission at the filesystem level, but does not make the file a functioning executable program. The `770` mode also applies to the file's owner and group; access still depends on the user's effective identity and the applicable filesystem permissions.

## Concepts Practiced

### RBAC — Role-Based Access Control

Role-Based Access Control (RBAC) is an access control model in which permissions are associated with roles, and users receive access to resources through their membership in those roles.

In a real environment, for example, a role could be defined as:

```text
Accounting
```

Users responsible for that function would then be assigned to the corresponding group or role.

In this activity, the following group was used to represent that function:

```text
contabilidade
```

**Clarification:** A Linux group can serve as a practical way to represent a role, but traditional Unix file permissions are primarily based on the owner, owning group, and other users. The exercise illustrates role-based access concepts rather than implementing a full RBAC system.

### Linux Groups

Groups allow users to be organized and access to shared resources to be controlled.

In this exercise:

```text
User:
teste1

Group:
contabilidade

File:
texto.txt
```

The relationship can be represented conceptually as:

```text
teste1
   │
   ▼
contabilidade
   │
   ▼
texto.txt
```

### `chmod 770`

The `770` permission grants full read, write, and execute permissions to the owner and the group, while removing permissions from other users.

```text
Owner   → rwx
Group   → rwx
Others  → ---
```

This restricts access according to the file's owner and group permissions.

## Results

The activity demonstrated how to create a dedicated group, add a user to that group, and assign the group as the owner of the file used in the laboratory.

The workflow was:

```text
Create group
    ↓
contabilidade
    ↓
Add user teste1
    ↓
Assign group to texto.txt
    ↓
Apply chmod 770
```

The file was configured to grant read, write, and execute permissions to its owner and members of the `contabilidade` group, while other users received no permissions.

## Evidence

The evidence for this activity corresponds to Step 9, after executing the following command:

```bash
chmod 770 texto.txt
```

[View Evidence — Classes 19–20](../evidencias.pdf)

---

[Back to Classes 19–20](../) · [Back to Module 05](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
