# Activity 4.06 — Implementing a RADIUS Server on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 04  
> **Class:** 15–16  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Implement and test a RADIUS (Remote Authentication Dial-In User Service) server using FreeRADIUS on Kali Linux.

The activity demonstrates a centralized authentication scenario in which a client sends an authentication request to a RADIUS server. Tests were performed using both a previously configured user and a nonexistent user, allowing the observation of an accepted authentication request and a rejected attempt.

The laboratory was performed in a controlled academic environment.

## Environment

- **Operating system:** Kali Linux
- **RADIUS server:** FreeRADIUS 3.2.3
- **Network interface:** `eth0`
- **Laboratory IP address:** `192.168.98.40`
- **Loopback address:** `127.0.0.1`
- **RADIUS authentication port:** `1812`
- **RADIUS accounting port:** `1813`
- **Testing tool:** `radtest`

The credentials used to access the course virtual machine are not documented in this README.

## Procedure

### 1. Obtain Administrative Access

A terminal was opened, and superuser access was obtained:

```bash
sudo -i
```

The password used for privilege elevation belongs to the laboratory environment and is not reproduced in this document.

### 2. Inspect Network Interfaces

The `ifconfig` command was used to inspect the available interfaces, particularly the loopback interface:

```bash
ifconfig
```

**Observed output:**

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:df:26:13:80  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::1005:27ff:fe44:1631  prefixlen 64  scopeid 0x20<link>
        ether 12:05:27:44:16:31  txqueuelen 1000  (Ethernet)
        RX packets 1818194  bytes 2694820836 (2.5 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61082  bytes 77348531 (73.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Ethernet)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
```

The main interfaces identified were:

- `docker0` — interface associated with the Docker network.
- `eth0` — network interface used by the virtual machine, with the address `192.168.98.40`.
- `lo` — loopback interface, using `127.0.0.1`.

The activity uses the loopback interface to perform local authentication tests.

### 3. Inspect FreeRADIUS Configuration Files

The FreeRADIUS configuration directory was listed using:

```bash
ls /etc/freeradius/3.0
```

**Observed output:**

```text
certs         experimental.conf  mods-available  panic.gdb
clients.conf  hints              mods-config      policy.d
dictionary    huntgroups         mods-enabled     proxy.conf
README.rst    radiusd.conf       sites-enabled    templates.conf
sites-available  trigger.conf    users
```

The directory contains the primary FreeRADIUS configuration files and subdirectories, including:

- `clients.conf` — configuration for RADIUS clients.
- `users` — file used in this laboratory to define the test user.
- `sites-enabled` — configuration for enabled virtual servers.
- `mods-enabled` — enabled modules.
- `radiusd.conf` — main service configuration file.

### 4. Inspect RADIUS Client Configuration

The client configuration file was inspected:

```bash
cat /etc/freeradius/3.0/clients.conf
```

The laboratory environment already contained a configured localhost client.

The relevant configuration shown in the laboratory instructions was:

```text
#  The default secret below is only for testing, and should
#  not be used in any real environment.
#
secret = testing123
```

The value `testing123` is a shared secret used by the RADIUS client and server to protect and validate communication in this test scenario.

**Security note:** This configuration is suitable only for the laboratory. A predictable shared secret must not be used in production. Real deployments should use a strong, unique secret and protect RADIUS traffic appropriately.

### 5. Create a Test User

The FreeRADIUS users file was edited:

```bash
nano /etc/freeradius/3.0/users
```

The following entry was added:

```text
usuario1 Cleartext-Password := "[senha definida no laboratório]"
```

The user `usuario1` was subsequently used to test a valid authentication request.

The original laboratory password is not published in this README.

After editing the file, the changes were saved using:

```text
Ctrl + X
S
ENTER
```

The password is represented by a placeholder and should be replaced only with the laboratory's actual test credential when reproducing the exercise in an authorized environment.

### 6. Start FreeRADIUS

The server was started in debug mode:

```bash
freeradius -X
```

The `-X` option is particularly useful in a laboratory because it displays detailed information about the processing of incoming requests in the terminal.

**Initial output:**

```text
FreeRADIUS Version 3.2.3
Copyright (C) 1999-2022 The FreeRADIUS server project and contributors
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE
You may redistribute copies of the software under the terms of the
GNU General Public License
For more information about these matters, see the file named COPYRIGHT
Starting - reading configuration files ...
including dictionary file /usr/share/freeradius/dictionary
including dictionary file /usr/share/freeradius/dictionary.dhcp

...

listen {
        type = "acct"
        ipv6addr = ::
        port = 0
   limit {
        max_connections = 16
        lifetime = 0
        idle_timeout = 30
   }
}
listen {
        type = "auth"
        ipaddr = 127.0.0.1
        port = 18120
}
Listening on auth address * port 1812 bound to server default
Listening on acct address * port 1813 bound to server default
Listening on auth address :: port 1812 bound to server default
Listening on acct address :: port 1813 bound to server default
Listening on auth address 127.0.0.1 port 18120 bound to server inner-tunnel
Listening on proxy address * port 43055
Listening on proxy address :: port 36998
Ready to process requests
```

The message:

```text
Ready to process requests
```

indicates that FreeRADIUS finished loading its configuration and was ready to receive requests.

In the observed configuration:

- **1812** — RADIUS authentication.
- **1813** — RADIUS accounting.
- **127.0.0.1:18120** — the `inner-tunnel` virtual server.

The debug process remained active while the tests were performed from a second terminal.

### 7. Test Authentication with a Valid User

A second terminal was used to run an authentication test with `radtest`:

```bash
radtest usuario1 [senha-do-laboratório] 127.0.0.1 0 testing123
```

**Observed output:**

```text
Sent Access-Request Id 246 from 0.0.0.0:af56 to 127.0.0.1:1812 length 78
        User-Name = "usuario1"
        User-Password = "[senha-do-laboratório]"
        NAS-IP-Address = 127.0.1.1
        NAS-Port = 0
        Message-Authenticator = 0x00
        Cleartext-Password = "[senha-do-laboratório]"
Received Access-Accept Id 246 from 127.0.0.1:714 to 127.0.0.1:44886 length 20
Message-Authenticator = 0xca5dfd87ba2b797e16edfe5c7ecb1d40
```

The most important result was:

```text
Received Access-Accept
```

This indicates that the RADIUS server accepted the authentication request.

#### Parameters Used

| Parameter | Purpose |
|---|---|
| `radtest` | Tool used to test RADIUS authentication |
| `usuario1` | User configured in FreeRADIUS |
| Test password | Credential configured for the laboratory user |
| `127.0.0.1` | RADIUS server address used for the test |
| `0` | NAS-Port value used by the test utility |
| `testing123` | Shared secret configured for the test client |

The test was performed against the local RADIUS server, avoiding the need for an external authentication endpoint.

### 8. Analyze the Accepted Authentication Log

The first terminal displayed the processing of the request by FreeRADIUS.

**Relevant log output:**

```text
Ready to process requests
(0)     Received Access-Request Id 246 from 127.0.0.1:40968 to 127.0.0.1:1812 length 78
(0)   Message-Authenticator = 0x80ae90efd30a3e6e0d4f9cac1c5a16b6
(0)   User-Name = "usuario1"
(0)   User-Password = "[senha-do-laboratório]"
(0)   NAS-IP-Address = 127.0.1.1
(0)   NAS-Port = 0
(0) # Executing section authorize from file /etc/freeradius/3.0/sites-enabled/default
(0)   authorize {
(0)     policy filter_username {
(0)       if (&User-Name) {
(0)       if (&User-Name)  -> TRUE
(0)       if (&User-Name)  {
(0)         if (&User-Name =~ / /) {
(0)         if (&User-Name =~ / /)  -> FALSE
(0)         if (&User-Name =~ /@[^@]*@/ ) {
(0)         if (&User-Name =~ /@[^@]*@/ )  -> FALSE
(0)         if (&User-Name =~ /\.\./ ) {
(0)         if (&User-Name =~ /\.\./ )  -> FALSE
(0)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))  {
(0)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))   -> FALSE
(0)         if (&User-Name =~ /\.$/)  {
(0)         if (&User-Name =~ /\.$/)   -> FALSE
(0)         if (&User-Name =~ /@\./)  {
(0)         if (&User-Name =~ /@\./)   -> FALSE
(0)       } # if (&User-Name)  = notfound
(0)     } # policy filter_username = notfound
(0)     [preprocess] = ok
(0)     [chap] = noop
(0)     [mschap] = noop
(0)     [digest] = noop
(0) suffix: Checking for suffix after "@"
(0) suffix: No '@' in User-Name = "usuario1", looking up realm NULL
(0) suffix: No such realm "NULL"
(0)     [suffix] = noop
(0) eap: No EAP-Message, not doing EAP
(0)     [eap] = noop
(0) files: users: Matched entry usuario1 at line 91
(0)     [files] = ok
(0)     [expiration] = noop
(0)     [logintime] = noop
(0)     [pap] = updated
(0)   } # authorize = updated
(0) Found Auth-Type = PAP
(0) # Executing group from file /etc/freeradius/3.0/sites-enabled/default
(0)   Auth-Type PAP {
(0)     pap: Login attempt with password
(0)     pap: Comparing with "known good" Cleartext-Password
(0)     pap: User authenticated successfully
(0)     [pap] = ok
(0)   } # Auth-Type PAP = ok
(0) # Executing section post-auth from file /etc/freeradius/3.0/sites-enabled/default
(0)   post-auth {
(0)     if (session-state:User-Name && reply:User-Name && request:User-Name && (reply:User-Name == request:User-Name)) {
(0)     if (session-state:User-Name && reply:User-Name && request:User-Name && (reply:User-Name == request:User-Name))  -> FALSE
(0)     update {
(0)       No attributes updated for RHS &session-state:
(0)     } # update = noop
(0)     [exec] = noop
(0)     policy remove_reply_message_if_eap {
(0)       if (&reply:EAP-Message && &reply:Reply-Message) {
(0)       if (&reply:EAP-Message && &reply:Reply-Message)  -> FALSE
(0)       else {
(0)         [noop] = noop
(0)       } # else = noop
(0)     } # policy remove_reply_message_if_eap = noop
(0)     if (EAP-Key-Name && &reply:EAP-Session-Id) {
(0)     if (EAP-Key-Name && &reply:EAP-Session-Id)  -> FALSE
(0)   } # post-auth = noop
(0) Sent Access-Accept Id 246 from 127.0.0.1:1812 to 127.0.0.1:44886 length 20
(0) Finished request
Waking up in 4.9 seconds.
(0) Cleaning up request packet ID 246 with timestamp +69 due to cleanup_delay was reached
Ready to process requests
```

#### Interpretation

The observed flow was:

1. FreeRADIUS received an `Access-Request`.
2. The `usuario1` account was found in the `users` file.
3. The entry was accepted by the `files` module.
4. The server selected `Auth-Type = PAP`.
5. The PAP module compared the supplied password with the configured credential.
6. Authentication completed successfully.
7. The server returned `Access-Accept`.

The most significant log line was:

```text
pap: User authenticated successfully
```

This was followed by:

```text
Sent Access-Accept
```

Together, these messages confirm that FreeRADIUS accepted the authentication request for the configured test user.

### 9. Test Authentication with a Nonexistent User

After the successful test, another authentication attempt was made with a username that had not been configured:

```bash
radtest usuarioX [senha-do-laboratório] 127.0.0.1 0 testing123
```

**Observed output:**

```text
Sent Access-Request Id 211 from 0.0.0.0:bd19 to 127.0.0.1:1812 length 78
        User-Name = "usuarioX"
        User-Password = "[senha-do-laboratório]"
        NAS-IP-Address = 127.0.1.1
        NAS-Port = 0
        Message-Authenticator = 0x00
        Cleartext-Password = "[senha-do-laboratório]"
Received Access-Reject Id 211 from 127.0.0.1:714 to 127.0.0.1:60653 length 20
        Message-Authenticator = 0xf9a00ead8e578adcede7fa8190a3bffb
(0) -: Expected Access-Accept got Access-Reject
```

The result differed from the previous test:

```text
Received Access-Reject
```

This demonstrates that the authentication request for the unconfigured user was rejected.

The final message from `radtest` indicates that the utility expected an `Access-Accept` but received an `Access-Reject`, which was the expected outcome for this test case.

### 10. Analyze the Rejected Authentication Log

The first terminal recorded the processing of the request:

```text
Ready to process requests
(1) Received Access-Request Id 211 from 127.0.0.1:60653 to 127.0.0.1:1812 length 78
(1)   Message-Authenticator = 0x82d0c1a625c7db2b6d59b94efb8b37ba
(1)   User-Name = "usuarioX"
(1)   User-Password = "[senha-do-laboratório]"
(1)   NAS-IP-Address = 127.0.1.1
(1)   NAS-Port = 0
(1) # Executing section authorize from file /etc/freeradius/3.0/sites-enabled/default
(1)   authorize {
(1)     policy filter_username {
(1)       if (&User-Name) {
(1)       if (&User-Name)  -> TRUE
(1)       if (&User-Name)  {
(1)         if (&User-Name =~ / /) {
(1)         if (&User-Name =~ / /)  -> FALSE
(1)         if (&User-Name =~ /@[^@]*@/ ) {
(1)         if (&User-Name =~ /@[^@]*@/ )  -> FALSE
(1)         if (&User-Name =~ /\.\./ ) {
(1)         if (&User-Name =~ /\.\./ )  -> FALSE
(1)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))  {
(1)         if ((&User-Name =~ /@/) && (&User-Name !~ /@(.+)\.(.+)$/))   -> FALSE
(1)         if (&User-Name =~ /\.$/)  {
(1)         if (&User-Name =~ /\.$/)   -> FALSE
(1)         if (&User-Name =~ /@\./)  {
(1)         if (&User-Name =~ /@\./)   -> FALSE
(1)       } # if (&User-Name)  = notfound
(1)     } # policy filter_username = notfound
(1)     [preprocess] = ok
(1)     [chap] = noop
(1)     [mschap] = noop
(1)     [digest] = noop
(1) suffix: Checking for suffix after "@"
(1) suffix: No '@' in User-Name = "usuarioX", looking up realm NULL
(1) suffix: No such realm "NULL"
(1)     [suffix] = noop
(1) eap: No EAP-Message, not doing EAP
(1)     [eap] = noop
(1)     [files] = noop
(1)     [expiration] = noop
(1)     [logintime] = noop
(1) pap: WARNING: No "known good" password found for the user.  Not setting Auth-Type
(1) pap: WARNING: Authentication will fail unless a "known good" password is available
(1)     [pap] = noop
(1)   } # authorize = ok
(1) ERROR: No Auth-Type found: rejecting the user via Post-Auth-Type = Reject
(1) Failed to authenticate the user
(1) Using Post-Auth-Type Reject
(1) # Executing group from file /etc/freeradius/3.0/sites-enabled/default
(1)   Post-Auth-Type REJECT {
(1)     attr_filter.access_reject: EXPAND %{User-Name}
(1)     attr_filter.access_reject:    --> usuarioX
(1)     attr_filter.access_reject: Matched entry DEFAULT at line 11
(1)     [attr_filter.access_reject] = updated
(1)     [eap] = noop
(1)     policy remove_reply_message_if_eap {
(1)       if (&reply:EAP-Message && &reply:Reply-Message) {
(1)       if (&reply:EAP-Message && &reply:Reply-Message)  -> FALSE
(1)       else {
(1)         [noop] = noop
(1)       } # else = noop
(1)     } # policy remove_reply_message_if_eap = noop
(1)   } # Post-Auth-Type REJECT = updated
(1) Delaying response for 1.000000 seconds
Waking up in 0.3 seconds.
Waking up in 0.6 seconds.
(1) Sending delayed response
(1) Sent Access-Reject Id 211 from 127.0.0.1:1812 to 127.0.0.1:60653 length 20
Waking up in 3.9 seconds.
(1) Cleaning up request packet ID 211 with timestamp +412 due to cleanup_delay was reached
Ready to process requests
```

#### Interpretation

Unlike `usuario1`, the `usuarioX` entry was not found in the configured users file.

The log shows this through:

```text
[files] = noop
```

and subsequently:

```text
pap: WARNING: No "known good" password found for the user.
```

Because no valid credential was associated with the requested account, the server did not set an authentication type:

```text
ERROR: No Auth-Type found: rejecting the user via Post-Auth-Type = Reject
```

Finally, the server sent:

```text
Sent Access-Reject
```

The second test therefore demonstrated how FreeRADIUS rejects an authentication request when no configured credential is available for the requested user.

## Commands Used

The following commands and configuration operations were used throughout the activity:

```bash
sudo -i
ifconfig
ls /etc/freeradius/3.0
cat /etc/freeradius/3.0/clients.conf
nano /etc/freeradius/3.0/users
freeradius -X
radtest usuario1 [senha-do-laboratório] 127.0.0.1 0 testing123
radtest usuarioX [senha-do-laboratório] 127.0.0.1 0 testing123
```

The two `radtest` commands were executed from a second terminal while the FreeRADIUS debug process remained active in the first terminal.

**Credential-handling note:** The password and the shared secret in these example commands are laboratory values. Avoid using real passwords directly in command-line arguments in production environments, because they may be exposed through shell history or process information.

## Concepts Practiced

### RADIUS

RADIUS is a protocol used for authentication, authorization, and accounting in network environments.

### FreeRADIUS

FreeRADIUS is an open-source implementation of the RADIUS protocol that can provide centralized authentication.

### Access-Request

A message sent by a client to a RADIUS server requesting authentication of a user.

### Access-Accept

A response indicating that the server accepted the authentication request.

### Access-Reject

A response indicating that the authentication request was rejected.

### Shared Secret

A secret shared between the RADIUS client and server, used as part of the protection and validation of RADIUS communication.

The laboratory used `testing123`, a weak value intended only for testing. Production environments require a strong, unique shared secret and appropriate network protections.

### PAP

Password Authentication Protocol was the authentication method observed during the test for the configured user.

The log included:

```text
Found Auth-Type = PAP
```

and:

```text
pap: User authenticated successfully
```

PAP is a protocol mechanism whose security depends on the protection of the communication channel and the surrounding RADIUS deployment. It should be configured only with suitable transport protections and within the requirements of the authentication environment.

### RADIUS Debugging

The `freeradius -X` command displays detailed processing information, allowing administrators to identify configuration issues and understand why authentication requests are accepted or rejected.

## Results

The activity demonstrated how to implement a FreeRADIUS server and validate its behavior using local authentication requests.

Two scenarios were tested:

| Scenario | Result |
|---|---|
| `usuario1` configured in FreeRADIUS | `Access-Accept` |
| `usuarioX` not configured in FreeRADIUS | `Access-Reject` |

The first test demonstrated the full flow of an accepted authentication request. The second showed how the server rejects a request when it cannot find a valid configured credential for the requested user.

The exercise reinforced the role of centralized authentication, RADIUS request/response messages, shared secrets, user configuration, and server-side debugging in network security.

## Evidence

The activity evidence is included in the PDF for Module 04, Classes 15–16.

**Recorded screenshot:** Step 11 of the activity, as specified by the general Module 04 evidence instructions.

[View Evidence — Classes 15–16](../evidencias.pdf)

---

[Back to Classes 15–16](../) · [Back to Module 04](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
