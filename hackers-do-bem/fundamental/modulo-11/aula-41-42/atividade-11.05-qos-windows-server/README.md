# Activity 11.05 — QoS on Windows Server 2022

## Objective

Configure a **Quality of Service (QoS)** policy on Windows Server 2022 using the **Local Group Policy Editor**, set an outbound traffic rate limit, and verify the configuration's impact through a speed test.

## Environment

- **Operating system:** Windows Server 2022
- **Access:** RDP
- **Tool:** Local Group Policy Editor
- **Configuration:** Policy-based QoS
- **Policy name:** `Teste`
- **Configured limit:** `1 MBps`

> A limit of `1 MBps` is approximately equivalent to `8 Mbps`, considering the conversion between bytes and bits.

## 1. Performing the Initial Speed Test

Windows Server 2022 was accessed via RDP.

First, Microsoft Edge was opened and the following website was accessed:

```text
https://www.minhaconexao.com.br/
```

A speed test was performed to establish a baseline before configuring QoS.

In the initial test, the **upload speed was above 20 Mbps**.

After the test, the browser was closed.

## 2. Opening the Local Group Policy Editor

The Windows search menu was used to locate:

```text
gpedit.msc
```

The **Local Group Policy Editor** was opened.

## 3. Accessing the QoS Settings

In the Local Group Policy Editor, the following path was accessed:

```text
Computer Configuration
└── Windows Settings
    └── Policy-based QoS
```

Under **Policy-based QoS**, the context menu was opened with a right-click, and the following option was selected:

```text
Create new policy
```

## 4. Creating the Policy

The wizard for creating a new QoS policy was launched.

The following name was entered in the policy name field:

```text
Teste
```

The policy was created with this name to make it easier to identify later.

## 5. Configuring the DSCP Value

During the DSCP configuration step, the following value was retained:

```text
0
```

DSCP (*Differentiated Services Code Point*) is used to mark packets according to different service classes.

In this lab, no specific DSCP marking was applied.

## 6. Enabling the Outbound Rate Limit

On the next screen, the following option was enabled:

```text
Specify Outbound Throttle Rate
```

The following value was entered:

```text
1 MBps
```

This setting establishes an outbound traffic rate limit associated with the policy.

For reference:

```text
1 byte = 8 bits
1 MB/s ≈ 8 Mb/s
```

Therefore, the configured limit represents approximately **8 Mbps** when converted to megabits per second.

## 7. Defining the Applications

On the application selection screen, the following option was selected:

```text
All applications
```

This ensured that the policy was not restricted to a specific application.

## 8. Defining the Source IP Address

On the source IP address configuration screen, the following option was selected:

```text
Any source IP address
```

This allows the policy to apply regardless of the source IP address.

## 9. Defining the Ports

On the port configuration screen, the following options were retained:

```text
From any source port
To any destination port
```

The policy was therefore not restricted to a specific source or destination port.

## 10. Completing the Policy

After reviewing the configuration, the wizard was completed.

The resulting policy had the following characteristics:

| Setting | Value |
|---|---|
| Name | `Teste` |
| DSCP | `0` |
| Outbound rate limit | `1 MBps` |
| Applications | All |
| Source IP address | Any |
| Source port | Any |
| Destination port | Any |

## 11. Verifying the Created Policy

In the **Local Group Policy Editor**, the following path was accessed again:

```text
Computer Configuration
→ Windows Settings
→ Policy-based QoS
```

The `Teste` policy appeared in the list of configured policies.

## 12. Performing Another Speed Test

Microsoft Edge was opened again, and the following website was accessed:

```text
https://www.minhaconexao.com.br/
```

Another speed test was performed to evaluate the connection's behavior after the policy was applied.

## 13. Comparing the Results with the Initial Test

In the first test, conducted before the policy was created, the upload speed was above **20 Mbps**.

After configuring the `Teste` policy, the observed upload speed was approximately:

```text
7–10 Mbps
```

This reduction is consistent with the lab's objective of applying a traffic limit of approximately `1 MBps`. However, actual speed test results may vary depending on connection conditions and the test server itself.

## 14. Recording the Speed Test Evidence

A speed test was performed again after the QoS policy was configured.

### Evidence — Step 14

**Caption to include before the screenshot:**

> Screenshot of Activity 11.05: the speed test performed after creating the `Teste` QoS policy, showing the upload speed behavior after applying the configured traffic rate limit.

[View Evidence — Classes 41–42](../evidencias.pdf)

## 15. Removing the QoS Policy

After recording the evidence, the browser was closed.

In the **Local Group Policy Editor**, the `Teste` policy was located under:

```text
Computer Configuration
→ Windows Settings
→ Policy-based QoS
```

The policy was right-clicked and removed by selecting:

```text
Delete
```

The deletion was confirmed by selecting:

```text
Yes
```

The traffic-limiting policy created during the lab was then removed.

## Key Concepts

- **QoS (Quality of Service):** A mechanism used to control and organize network traffic.
- **Policy-based QoS:** Allows traffic control policies to be applied through Windows Group Policy settings.
- **DSCP:** A field used for IP traffic classification.
- **Outbound Throttle:** A mechanism for limiting the outbound traffic rate.
- **Mbps:** Megabits per second.
- **MBps/MB/s:** Megabytes per second.

## Activity Workflow

```text
Perform the initial speed test
          ↓
Open gpedit.msc
          ↓
Access Policy-based QoS
          ↓
Create the "Teste" policy
          ↓
DSCP = 0
          ↓
Rate limit = 1 MBps
          ↓
Apply to all applications
          ↓
Any IP address and any port
          ↓
Perform another speed test
          ↓
Compare the results
          ↓
Remove the policy
```

## Result

A **Policy-based QoS** policy named `Teste` was created and configured to limit outbound traffic to `1 MBps`. After the policy was applied, the speed test showed an upload speed in the range of **7–10 Mbps**, compared with more than **20 Mbps** in the initial test. The policy was removed at the end of the activity.

---

[Back to Classes 41–42](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
