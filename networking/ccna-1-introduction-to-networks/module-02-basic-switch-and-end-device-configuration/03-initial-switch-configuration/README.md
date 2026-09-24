# Lab 03 — Initial Switch Configuration

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/aa6614c5-83e8-4946-9124-79020889b68a" />

## Overview

This Packet Tracer lab introduced the initial configuration of a Cisco Catalyst 2960 switch.

The lab focused on securing CLI access, configuring privileged EXEC authentication, encrypting passwords, creating a Message of the Day (MOTD) banner, saving the configuration to NVRAM, and applying the same configuration principles to a second switch.

## Objectives

* Verify the default switch configuration
* Configure a hostname
* Secure console access
* Configure privileged EXEC passwords
* Configure an encrypted privileged EXEC secret
* Encrypt plaintext passwords
* Configure a MOTD banner
* Save the running configuration to NVRAM
* Verify the startup configuration
* Configure a second switch using the same principles

---

## Lab Environment

### Network Devices

* Cisco Catalyst 2960 — S1
* Cisco Catalyst 2960 — S2

### Management

* Cisco IOS CLI
* Packet Tracer

---

# Part 1 — Verify the Default Switch Configuration

## Enter Privileged EXEC Mode

The switch was accessed through the CLI and the `enable` command was used:

```text
Switch> enable
Switch#
```

The prompt changed from User EXEC mode to Privileged EXEC mode.

## Examine the Running Configuration

The current configuration was examined using:

```text
Switch# show running-config
```

### Configuration Findings

**Fast Ethernet interfaces:**

```text
24
```

**Gigabit Ethernet interfaces:**

```text
2
```

**VTY line range:**

```text
0–4
```

**Command used to display the startup configuration:**

```text
show startup-config
```

**Why does the switch display `startup-config is not present`?**

The switch does not have a startup configuration saved in NVRAM yet. The configuration exists only in the running configuration.

---

# Part 2 — Basic Switch Configuration

## Configure Hostname

The switch hostname was changed from the default name to `S1`:

```text
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# exit
S1#
```

The hostname is reflected in the CLI prompt.

---

## Secure Console Access

Console access was protected using a password:

```text
S1# configure terminal
S1(config)# line console 0
S1(config-line)# password letmein
S1(config-line)# login
S1(config-line)# exit
S1(config)# exit
```

### Why is `login` required?

The `password` command defines the password, but the `login` command tells IOS to require that password when a user accesses the console line.

---

## Verify Console Authentication

The privileged EXEC session was exited to verify the console password:

```text
S1# exit
```

The switch then displayed:

```text
User Access Verification

Password:
```

The configured console password was required before access to User EXEC mode was granted.

---

## Configure Privileged EXEC Password

A plaintext enable password was configured:

```text
S1> enable
S1# configure terminal
S1(config)# enable password c1$c0
S1(config)# exit
```

The password protects access to Privileged EXEC mode.

---

## Configure Enable Secret

An `enable secret` was configured to replace the plaintext enable password as the authentication method for Privileged EXEC mode:

```text
S1# configure terminal
S1(config)# enable secret itsasecret
S1(config)# exit
```

When both `enable password` and `enable secret` are configured, IOS uses the `enable secret` password for Privileged EXEC authentication.

---

## Verify Password Configuration

The running configuration was examined:

```text
S1# show running-config
```

The `enable secret` appeared in an encrypted form rather than as:

```text
itsasecret
```

### Why is `enable secret` displayed differently?

The `enable secret` is stored using a cryptographic hash rather than as plaintext. This provides stronger protection than the legacy `enable password` command.

---

## Encrypt Plaintext Passwords

The `service password-encryption` command was used:

```text
S1# configure terminal
S1(config)# service password-encryption
S1(config)# exit
```

This encrypts plaintext passwords such as the console password and legacy enable password in the configuration.

### Result

New passwords configured using password-based commands covered by this feature will be stored in an encrypted form rather than plaintext.

> **Note:** `service password-encryption` provides basic obfuscation and should not be confused with strong cryptographic password hashing provided by `enable secret`.

---

# Part 3 — Configure MOTD Banner

A Message of the Day banner was configured:

```text
S1# configure terminal
S1(config)# banner motd "This is a secure system. Authorized Access Only!"
S1(config)# exit
```

### When is the MOTD banner displayed?

The banner is displayed when users connect to the device before being granted access to the CLI.

### Why configure a MOTD banner?

A MOTD banner can:

* Warn unauthorized users that access is prohibited
* Provide an administrative or security notice
* Establish an explicit access policy
* Support organizational security requirements

---

# Part 4 — Save and Verify the Configuration

## Verify the Running Configuration

The completed configuration was reviewed using:

```text
S1# show running-config
```

## Save Configuration to NVRAM

The running configuration was saved as the startup configuration:

```text
S1# copy running-config startup-config
```

When prompted:

```text
Destination filename [startup-config]?
```

`ENTER` was pressed to accept the default filename.

The switch confirmed:

```text
Building configuration...
[OK]
```

### Short Form

The command can be abbreviated as:

```text
copy run start
```

## Verify the Startup Configuration

The configuration stored in NVRAM was displayed using:

```text
S1# show startup-config
```

The saved configuration was verified to contain the configured settings.

---

# Part 5 — Configure S2

The same configuration principles were applied to the second switch.

### S2 Configuration Requirements

| Parameter            | Configuration           |
| -------------------- | ----------------------- |
| Hostname             | `S2`                    |
| Console password     | `letmein`               |
| Enable password      | `c1$c0`                 |
| Enable secret        | `itsasecret`            |
| MOTD                 | Security/access warning |
| Password encryption  | Enabled                 |
| Configuration backup | Saved to NVRAM          |

The final configuration was verified and saved using:

```text
S2# show running-config
S2# copy running-config startup-config
S2# show startup-config
```

---

## Key Commands

| Purpose                        | Command                              |
| ------------------------------ | ------------------------------------ |
| Enter Privileged EXEC          | `enable`                             |
| Enter Global Configuration     | `configure terminal`                 |
| Configure hostname             | `hostname S1`                        |
| Configure console line         | `line console 0`                     |
| Configure console password     | `password letmein`                   |
| Require console authentication | `login`                              |
| Configure enable password      | `enable password c1$c0`              |
| Configure enable secret        | `enable secret itsasecret`           |
| Encrypt plaintext passwords    | `service password-encryption`        |
| Configure MOTD                 | `banner motd "message"`              |
| View running configuration     | `show running-config`                |
| View startup configuration     | `show startup-config`                |
| Save configuration             | `copy running-config startup-config` |



