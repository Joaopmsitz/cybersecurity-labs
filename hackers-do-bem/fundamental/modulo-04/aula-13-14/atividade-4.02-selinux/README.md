# Activity 4.02 — Exploring SELinux on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 13–14  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Explore SELinux (Security-Enhanced Linux) on Kali Linux and understand how it works as a mandatory access control (MAC) mechanism.

The activity covered SELinux activation, status verification, and configuration inspection, including its operating mode, users, login mappings, Boolean variables, and port types.

**Important:** The laboratory instructions warn that incorrect SELinux configuration changes can make the environment inaccessible. All procedures were performed exclusively in the academic laboratory.

## Environment

- **Operating system:** Kali Linux
- **Tools:** `selinux-activate`, `sestatus`, `semanage`
- **Security mechanism:** SELinux
- **Observed policy:** `default`

## Procedure

### 1. Obtain Administrative Access

Administrative access to the system was obtained using:

```bash
sudo -i
```

The `sudo -i` command starts a shell with administrative privileges, allowing the commands required to configure and inspect SELinux to be executed.

### 2. Activate SELinux

SELinux was activated using:

```bash
selinux-activate
```

**Observed output:**

```text
Activating SE Linux
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-6.5.0-kali3-cloud-amd64
Found initrd image: /boot/initrd.img-6.5.0-kali3-cloud-amd64
Found linux image: /boot/vmlinuz-6.1.0-kali7-cloud-amd64
Found initrd image: /boot/initrd.img-6.1.0-kali7-cloud-amd64
Found linux image: /boot/vmlinuz-6.1.0-kali5-cloud-amd64
Found initrd image: /boot/initrd.img-6.1.0-kali5-cloud-amd64
done
SE Linux is activated.  You may need to reboot now.
```

The command activated SELinux and regenerated the GRUB configuration, identifying the kernels and corresponding initrd images available on the system.

The final message:

```text
SE Linux is activated.  You may need to reboot now.
```

indicates that a reboot may be required for the configuration to take effect.

### 3. Reboot the System

The system was restarted using:

```bash
reboot
```

During startup, SELinux may relabel the filesystem to apply the required security contexts.

The laboratory instructions provided output similar to the following:

```text
*** Warning -- SELinux default policy relabel is requires.
*** Relabeling could take a very long time, dependeing on file
*** system size and speed of hard drives.
libsemanage.add_user: user sddm not in password file
Warning: Skipping the following R/O filesystems:
/run/credentials/systemd-sysctl.service
/run/credentials/systemd-sysusers.service
/run/credentials/systemd-tmpfiles-setup-dev.service
/run/credentials/systemd-tmpfiles-setup.service
Relabeling /
75.5%
```

Filesystem relabeling applies SELinux security contexts to files and system resources.

Because the remote environment loses its connection during a reboot, this step may not be directly visible from the RDP session.

The output above is retained as recorded in the laboratory instructions, including the original messages and spelling.

### 4. Verify SELinux Status

After waiting for the time indicated by the laboratory and starting Kali Linux again, the SELinux status was checked:

```bash
sestatus
```

**Observed output:**

```text
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             default
Current mode:                   permissive
Mode from config file:          permissive
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Memory protection checking:     actual (secure)
Max kernel policy version:      33
```

#### Interpretation

- **SELinux status: enabled** — SELinux is enabled.
- **SELinuxfs mount: `/sys/fs/selinux`** — mount point for the filesystem used by SELinux.
- **SELinux root directory: `/etc/selinux`** — directory containing SELinux configuration.
- **Loaded policy name: `default`** — name of the loaded policy.
- **Current mode: `permissive`** — policy violations are recorded, but access is not blocked by SELinux enforcement.
- **Mode from config file: `permissive`** — the configured mode is also permissive.
- **Policy MLS status: enabled** — MLS-related support is enabled.
- **Policy deny_unknown status: allowed** — the reported policy setting permits unknown permissions or policy elements according to this status.
- **Memory protection checking: actual (secure)** — memory protection checking is reported as active in the installed configuration.
- **Max kernel policy version: `33`** — maximum policy version supported by the reported kernel interface.

#### Enforcing vs. Permissive

SELinux supports different operating modes. The two main modes covered in the laboratory were:

**Enforcing**

- SELinux policies are enforced.
- Accesses prohibited by the applicable policy can be blocked.
- Policy violations may also be logged.

**Permissive**

- SELinux evaluates policy rules and can log violations.
- Accesses are not blocked on the basis of those violations.

The laboratory showed SELinux running in **permissive** mode after activation.

### 5. Inspect SELinux Users

The `semanage` tool was used to list SELinux users:

```bash
semanage user -l
```

**Observed output:**

```text
                Rótulo     MLS/       MLS/                          
Usuário do SELinux Prefixo    Nível MCS  Intervalo MCS                  Funções do SELinux

guest_u         user       s0         s0                             guest_r
root            sysadm     s0         s0-s0:c0.c1023                 staff_r sysadm_r system_r
staff_u         staff      s0         s0-s0:c0.c1023                 staff_r sysadm_r
sysadm_u        sysadm     s0         s0-s0:c0.c1023                 sysadm_r
system_u        user       s0         s0-s0:c0.c1023                 system_r
unconfined_u    unconfined s0         s0-s0:c0.c1023                 system_r unconfined_r
user_u          user       s0         s0                             user_r
xdm             user       s0         s0                             system_r xdm_r
xguest_u        user       s0         s0                             xguest_r
```

The query displays the relationship between SELinux users, their levels, and their available roles.

Some roles shown in the output include:

- `guest_r` — role intended for guest users.
- `staff_r` — role associated with staff users.
- `sysadm_r` — administrative role.
- `system_r` — role used by system processes and components.
- `unconfined_r` — role with fewer SELinux restrictions.
- `user_r` — role intended for regular users.
- `xdm_r` — role associated with the graphical display manager.
- `xguest_r` — role intended for guest environments with additional restrictions.

SELinux identities and roles are distinct from ordinary Linux usernames and groups. Their effective access depends on the policy and the context in which they are used.

### 6. Inspect Login Mappings

The mappings between login accounts and SELinux users were inspected using:

```bash
semanage login -l
```

**Observed output:**

```text
Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
root                 unconfined_u         s0-s0:c0.c1023       *
sddm                 xdm                  s0-s0                *
```

The table contains the following fields:

- **Login Name:** account used for login.
- **SELinux User:** SELinux identity associated with the account.
- **MLS/MCS Range:** range of security levels or categories.
- **Service:** service to which the mapping applies.

In this environment:

- `__default__` maps to `unconfined_u`.
- `root` maps to `unconfined_u`.
- `sddm` maps to the SELinux user `xdm`.

These mappings determine which SELinux identity is assigned to a login account during the relevant login process.

### 7. Inspect SELinux Boolean Variables

The following command was used:

```bash
semanage boolean -l
```

The command returns a large list of SELinux Boolean variables. Examples from the observed output include:

```text
SELinux boolean                State  Default Description

aide_mmap_files                (off  ,  off)  Control if AIDE can mmap files. AIDE can be compiled with the option 'with-mmap' in which case it will attempt to mmap files while running.
allow_cvs_read_shadow          (off  ,  off)  Determine whether cvs can read shadow password files.
allow_execheap                 (off  ,  off)  Allow unconfined executables to make their heap memory executable.  Doing this is a really bad idea. Probably indicates a badly coded executable, but could indicate an attack. This executable should be reported in bugzilla
allow_execmem                  (off  ,  off)  Allow unconfined executables to map a memory region as both executable and writable, this is dangerous and the executable should be reported in bugzilla")

…

xguest_use_bluetooth           (off  ,  off)  Determine whether xguest can use blue tooth devices.
xscreensaver_read_generic_user_content (on   ,   on)  Grant the xscreensaver domains read access to generic user content
xserver_allow_dri              (off  ,  off)  Allow DRI access
xserver_can_network            (off  ,  off)  Allows the X server to use TCP/IP networking functionality (insecure).
xserver_client_writes_xserver_tmpfs (off  ,  off)  Allows clients to write to the X server tmpfs files.
xserver_gnome_xdm              (off  ,  off)  Use gnome-shell in gdm mode in gdm mode as the X Display Manager (XDM)
xserver_object_manager         (off  ,  off)  Support X userspace object manager
xserver_xdm_can_network        (off  ,  off)  Allows the X display manager to use TCP/IP networking functionality (insecure).
zabbix_can_network             (off  ,  off)  Determine whether zabbix can connect to all TCP ports
```

The main columns are:

- **SELinux boolean:** name of the Boolean variable.
- **State:** current state.
- **Default:** default state.
- **Description:** purpose of the variable.

Boolean variables allow specific SELinux policy behaviors to be adjusted without necessarily replacing or rewriting the entire policy.

The output above contains a shortened middle section, represented by the ellipsis as in the laboratory notes.

### 8. Inspect SELinux Port Definitions

The final configuration query listed port definitions known to SELinux:

```bash
semanage port -l
```

The output showed the SELinux port type, protocol, and port number:

```text
SELinux Port Type              Proto    Port Number

afs3_callback_port_t           tcp      7001
afs3_callback_port_t           udp      7001
afs_bos_port_t                 udp      7007

...

zookeeper_client_port_t        tcp      2181
zookeeper_election_port_t      tcp      3888
zookeeper_leader_port_t        tcp      2888
zope_port_t                    tcp      8021
```

This mapping allows SELinux policies to associate port types with particular services and protocols.

The main fields are:

- **SELinux Port Type:** security type associated with the port.
- **Proto:** protocol used, such as TCP or UDP.
- **Port Number:** numeric port identifier.

The displayed entries are examples from the available output. The full command can return many additional port definitions.

### 9. SELinux Deactivation — Optional Step

The laboratory instructions include an optional step for disabling SELinux, intended exclusively for a local virtual machine and not for the Hackers do Bem remote environment.

For this reason, **this change should not be performed on shared laboratory VMs**.

The procedure described in the instructions consists of changing:

```text
SELINUX=permissive
```

to:

```text
SELINUX=disabled
```

in the configuration file:

```text
/etc/selinux/config
```

and then rebooting the system.

After SELinux is disabled, `sestatus` may display:

```text
SELinux status:                 disabled
```

This optional step illustrates how persistent SELinux configuration can be changed. It was not part of the recommended procedure for the course's remote environment.

Disabling SELinux removes an important security control. The setting should only be modified in an authorized local test environment where the consequences are understood and recovery access is available.

## Commands Used

The following commands were used during the activity:

```bash
sudo -i
selinux-activate
reboot
sestatus
semanage user -l
semanage login -l
semanage boolean -l
semanage port -l
```

The optional configuration file discussed in the laboratory instructions was:

```text
/etc/selinux/config
```

## Concepts Practiced

### SELinux

Security-Enhanced Linux is a security mechanism that implements mandatory access control (MAC), adding security policies and contexts beyond conventional Linux user and group permissions.

### MAC — Mandatory Access Control

A model in which access decisions are governed by security policies rather than relying exclusively on standard filesystem permissions.

### Permissive Mode

A mode in which SELinux records policy violations but does not block access based on those violations.

### Enforcing Mode

A mode in which SELinux policies are actively enforced and unauthorized access can be blocked.

### `sestatus`

A command used to inspect SELinux status, the loaded policy, and the current operating mode.

### `semanage`

A tool used to administer aspects of SELinux policy configuration, including users, login mappings, Boolean variables, and ports.

### SELinux Boolean Variables

Variables that allow specific security policy behaviors to be enabled or disabled without requiring a complete policy rewrite.

### Security Contexts and Types

SELinux uses additional security information to determine how users, processes, files, and other resources may interact.

### Filesystem Relabeling

Relabeling applies the security contexts expected by the SELinux policy to filesystem objects. This can be required when SELinux is first enabled or when policy and labeling configurations change.

## Results

The activity provided a practical introduction to SELinux on Kali Linux and demonstrated how this mechanism complements the traditional Linux permission model.

The following operations and configurations were examined:

- SELinux activation.
- Status and operating mode.
- Loaded security policy.
- SELinux users.
- Mappings between login accounts and SELinux users.
- Boolean variables.
- Port types.
- Persistent configuration settings.

The activity also demonstrated the difference between **permissive** and **enforcing** modes and showed how `semanage` can be used to inspect multiple components of SELinux policy.

The recorded status showed that SELinux was enabled and operating in permissive mode. This means that policy violations could be logged without being blocked by SELinux enforcement.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 13–14.

**Recorded screenshot:** Step 5 of the activity, as required by the laboratory instructions, showing the SELinux status query using `sestatus`.

[View Evidence — Classes 13–14](../evidencias.pdf)

---

[Back to Classes 13–14](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
