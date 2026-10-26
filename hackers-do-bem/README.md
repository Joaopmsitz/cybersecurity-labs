# Activity 11.07 — Blocking Websites Using iptables on Kali Linux

## Objective

Use `iptables` on Kali Linux to create a firewall rule that blocks access to the `globo.com.br` domain, verify the rule, and subsequently remove it to restore access to the website.

## Environment

- **Operating system:** Kali GNU/Linux
- **Access:** RDP
- **Network interface:** `eth0`
- **Tool:** `iptables`
- **Website used for testing:** `globo.com.br`

## 1. Accessing Kali Linux

Kali Linux was started and accessed via RDP.

After opening the Terminal, administrative privileges were obtained using:

```bash
sudo -i
```

Authentication was completed using the user's password.

## 2. Opening the Browser in Private Browsing Mode

Mozilla Firefox was opened through the following menu:

```text
Applications → Web Browser
```

Next, the following keyboard shortcut was used:

```text
Ctrl + Shift + P
```

This opened a private browsing window.

## 3. Testing Website Access

In the Firefox private browsing window, the following website was accessed:

```text
www.globo.com.br
```

The website loaded normally before the blocking rule was applied.

This test established that the connection was working normally before the firewall configuration was changed.

## 4. Closing the Browser and Creating the Blocking Rule

After confirming that the website was accessible, all Mozilla Firefox windows were closed.

The following `iptables` rule was created in the Terminal:

```bash
iptables -A INPUT -s globo.com.br -j DROP
```

The added rule applies to the `INPUT` chain.

### Parameters Used

**`iptables`**

A tool used to configure packet-filtering rules for Netfilter, the Linux kernel's firewall framework.

**`-A INPUT`**

The `-A` parameter stands for Append and adds a new rule to the `INPUT` chain.

The `INPUT` chain processes packets destined for the local system.

**`-s globo.com.br`**

The `-s` parameter specifies the source of the packets to which the rule applies.

In this lab, the following hostname was used:

```text
globo.com.br
```

`iptables` resolves the hostname to its corresponding address when the rule is configured.

**`-j DROP`**

Specifies the action taken by the rule.

`DROP` causes matching packets to be discarded rather than accepted by the system.

The complete rule can be represented as follows:

```text
Packets originating from globo.com.br
              ↓
          INPUT chain
              ↓
             DROP
              ↓
       Packet discarded
```

## 5. Displaying the iptables Rules

To verify the current firewall configuration, the following command was executed:

```bash
iptables -L
```

The output was:

```text
┌──(root㉿kali)-[~]
└─# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
DROP       all  --  186-192-83-5.prt.globo.com  anywhere

Chain FORWARD (policy DROP)
target     prot opt source               destination
DOCKER-USER  all  --  anywhere             anywhere
DOCKER-ISOLATION-STAGE-1  all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere             ctstate RELATED,ESTABLISHED
DOCKER     all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination

Chain DOCKER (1 references)
target     prot opt source               destination

Chain DOCKER-ISOLATION-STAGE-1 (1 references)
target     prot opt source               destination
DOCKER-ISOLATION-STAGE-2  all  --  anywhere             anywhere
RETURN     all  --  anywhere             anywhere

Chain DOCKER-ISOLATION-STAGE-2 (1 references)
target     prot opt source               destination
DROP       all  --  anywhere             anywhere
RETURN     all  --  anywhere             anywhere

Chain DOCKER-USER (1 references)
target     prot opt source               destination
RETURN     all  --  anywhere             anywhere
```

In the `INPUT` chain, the added rule appeared as:

```text
DROP       all  --  186-192-83-5.prt.globo.com  anywhere
```

This shows that a rule was added to discard packets matching the source address resolved from the hostname used in the lab.

### Evidence — Step 6

**Caption to include before the screenshot:**

> Screenshot of Activity 11.07: the `iptables` rule listing, showing the `DROP` rule added to the `INPUT` chain to block traffic associated with the `globo.com.br` domain.

[View Evidence — Classes 43–44](../evidencias.pdf)

## 6. Testing Website Access Again

After creating the rule, Mozilla Firefox was opened again in private browsing mode.

The following website was accessed:

```text
www.globo.com.br
```

Unlike the first test, the website did not load normally.

According to the lab results, this behavior occurred because the `iptables` rule discarded packets matching the specified source address.

The observed behavior demonstrated the effect attributed to the filtering rule created during the activity.

## 7. Removing the Blocking Rule

After verifying the reported blocking behavior, the Terminal was opened again, and the rule was removed using:

```bash
iptables -D INPUT -s globo.com.br -j DROP
```

The parameter:

```text
-D
```

stands for Delete and removes an existing rule from the chain.

The remaining parameters correspond to the rule previously added:

```text
INPUT
-s globo.com.br
-j DROP
```

Therefore, the command removes the specific rule created at the beginning of the activity.

## 8. Verifying the Rules Again

After removing the blocking rule, the following command was executed:

```bash
iptables -L
```

The `INPUT` chain no longer displayed the `DROP` rule created for the domain:

```text
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
```

The other chains associated with the Docker environment remained present.

## 9. Confirming Website Access Again

After removing the rule, Mozilla Firefox was opened again, and the following address was accessed:

```text
www.globo.com.br
```

The website loaded normally again, demonstrating that the blocking rule had been removed.

After verifying access, the browser was closed.

## 10. Restarting Kali Linux

To finish the activity, the system was restarted using:

```bash
reboot
```

## Key Concepts

- **`iptables`:** A tool for configuring the Netfilter firewall on Linux.
- **Netfilter:** A framework in the Linux kernel for packet filtering and processing.
- **`INPUT`:** A chain that processes traffic destined for the local system.
- **`OUTPUT`:** A chain that processes traffic generated by the local system.
- **`DROP`:** Discards packets matching a rule.
- **`-A`:** Adds a rule to a chain.
- **`-D`:** Removes a rule from a chain.
- **`-s`:** Specifies the source address of packets.

## Activity Workflow

```text
Access globo.com.br
        ↓
Website loads normally
        ↓
Create the DROP rule
        ↓
Run iptables -L
        ↓
Website stops loading
        ↓
Remove the rule
        ↓
Run iptables -L
        ↓
Website loads again
```

## Result

An `iptables` rule was created to discard traffic associated with `globo.com.br`. After the rule was applied, access to the website was reported as blocked. The rule was then removed, and website access returned to normal.

### Technical Note

The command used in this activity adds a rule to the `INPUT` chain, which filters packets arriving at Kali Linux. It does not directly block outgoing requests from Kali Linux to the website. For reliable outbound blocking, a rule generally needs to target the `OUTPUT` chain and the destination IP address. Additionally, a hostname supplied to `iptables` is resolved when the rule is created, so the rule may not cover other addresses returned by DNS later.

---

[Back to Classes 43–44](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
