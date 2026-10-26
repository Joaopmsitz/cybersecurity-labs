# Activity 11.06 — Exploring ACLs in Windows Server 2022 Firewall

## Objective

Explore the advanced settings of Windows Server 2022 Firewall by examining inbound and outbound rules, connection security rules, and monitoring options related to the firewall and the security associations used in protected communications.

## Environment

- **Operating system:** Windows Server 2022
- **Access:** RDP
- **Tool:** Windows Defender Firewall with Advanced Security
- **Server IP address:** `192.168.98.30`

## 1. Accessing Windows Server 2022

Windows Server 2022 was started and accessed via RDP.

The machine used in the lab has the following IP address:

```text
192.168.98.30
```

After accessing the system, the Windows search field was opened using:

```text
Type here to search
```

The following tool was searched for:

```text
Windows Defender Firewall with Advanced Security
```

The **Windows Defender Firewall with Advanced Security** tool was then opened.

## 2. Exploring Inbound Rules

In the tool's left-hand pane, the following option was selected:

```text
Inbound Rules
```

Inbound Rules control traffic arriving at the computer or server.

These rules can allow or block incoming connections based on various criteria, such as:

- Application
- Service
- Protocol
- Port
- Source IP address
- Destination IP address
- Network profile
- Action defined by the rule

For example, a rule can allow a specific program to accept connections from other devices on the network.

## 3. Exploring Outbound Rules

In the left-hand pane, the following option was selected:

```text
Outbound Rules
```

Outbound Rules control traffic leaving the computer or server toward other devices, servers, or the Internet.

As with inbound rules, rules can be created using different criteria to allow or block outgoing connections.

One possible use is to create a rule that prevents a specific application or service from connecting to a particular destination.

## 4. Exploring Connection Security Rules

Next, the following option was selected:

```text
Connection Security Rules
```

Connection Security Rules define security requirements for specific communications between devices.

They can be used in scenarios involving:

- VPN
- IPsec
- Authentication
- Encryption
- Protection of communications between hosts

Unlike traditional firewall rules, which directly control whether traffic is allowed or blocked, connection security rules can define the requirements for establishing protected communications.

## 5. Exploring Monitoring

In the left-hand pane, the following option was selected:

```text
Monitoring
```

The Monitoring section provides information about firewall operation and the security rules configured on the system.

This section is useful for checking configuration status and reviewing information related to connections and applied policies.

## 6. Exploring Firewall Under Monitoring

The Monitoring section was expanded, and the following option was selected:

```text
Firewall
```

This section displays information related to the operation of firewall rules.

The information that can be reviewed includes:

### Allowed Connections

Displays connections permitted by the firewall's inbound or outbound rules.

### Blocked Connections

Displays connections prevented by firewall rules.

### Active Firewall Rules

Allows users to review the rules currently active and applied to the system.

### Connection Details

When a connection is selected, information about the communication may be displayed, including:

- Application involved
- IP address
- Port
- Traffic direction
- Other connection parameters

## 7. Exploring Connection Security Rules in Monitoring

Within Monitoring, the following option was expanded:

```text
Connection Security Rules
```

This section displays information related to connections that use security rules.

Depending on the environment and whether any connections have been configured or established, this section may be empty.

The information that may be available includes:

### Established Connections

Displays security connections established according to the configured rules.

### Dropped Connections

Displays connection attempts that were dropped or blocked by security rules.

### Connection Details

When a connection is available, the following information may be displayed:

- Devices involved
- Networks involved
- Authentication method
- Connection state
- Security parameters used

## 8. Accessing Security Associations

Within the Monitoring section, the following option was expanded:

```text
Security Associations
```

This section displays information about the Security Associations (SAs) used in protected communications.

The following options related to IPsec negotiation modes were observed:

```text
Security Associations
├── Main Mode
└── Quick Mode
```

## 9. Exploring Main Mode

The following path was accessed:

```text
Monitoring
→ Security Associations
→ Main Mode
```

The **Main Mode** section was opened.

Main Mode is associated with the initial negotiation process used by IKE (Internet Key Exchange) to establish security parameters between devices.

This negotiation can involve the following stages:

### Authentication

The devices involved authenticate their identities to establish a trusted relationship.

### Parameter Negotiation

The devices negotiate the cryptographic parameters used for secure communication.

These parameters may include:

- Encryption algorithms
- Authentication algorithms
- Key exchange parameters
- Security Association lifetimes

### Establishing the Security Association

After negotiation and authentication, the parameters required for protected communication are established.

The Main Mode section allows users to review information related to these negotiations, including details about the devices involved, security parameters, and the state of the associations.

### Evidence — Step 9

**Caption to include before the screenshot:**

> Screenshot of Activity 11.06: the Security Associations → Main Mode monitoring screen in Windows Server 2022 Firewall, displaying information related to security negotiations performed by IKE.

[View Evidence — Classes 43–44](../evidencias.pdf)

> **Observation:** Depending on the lab environment, the list of associations may be empty if no IPsec negotiation is active. The objective of this step is to display the screen requested by the lab instructions.

## 10. Exploring Quick Mode

After recording the evidence, the following path was accessed:

```text
Monitoring
→ Security Associations
→ Quick Mode
```

Quick Mode is used after the initial Main Mode negotiation to establish or update security associations specific to protected traffic.

Its functions include:

### Key Renewal

Allows new encryption and authentication keys to be established when necessary.

### Defining Protected Traffic

Parameters are defined for the traffic that will use the security association's protection.

These may include:

- IP addresses
- Ports
- Protocols
- Communication scope

### Communication Integrity

The negotiated parameters may also include mechanisms used to ensure the integrity of transmitted data.

The Quick Mode section allows users to review information related to these negotiations and the security associations established at this stage.

## 11. Closing the Activity

After exploring the different sections of Windows Server 2022 Firewall, all windows were closed.

## Key Concepts

- **ACL (Access Control List):** A set of rules used to control access and network traffic.
- **Firewall:** A mechanism that controls network connections according to configured rules.
- **Inbound Rules:** Rules applied to incoming traffic.
- **Outbound Rules:** Rules applied to outgoing traffic.
- **Connection Security Rules:** Rules used to define security requirements for communications.
- **IPsec:** A suite of protocols used to protect IP communications.
- **IKE (Internet Key Exchange):** A protocol used to negotiate parameters and establish security associations.
- **Main Mode:** The initial negotiation stage for security parameters.
- **Quick Mode:** A stage used to establish or update security associations specific to traffic.

## Activity Workflow

```text
Windows Defender Firewall with Advanced Security
          ↓
Inbound Rules
          ↓
Outbound Rules
          ↓
Connection Security Rules
          ↓
Monitoring
          ↓
Firewall
          ↓
Connection Security Rules
          ↓
Security Associations
     ↙             ↘
Main Mode       Quick Mode
```

## Result

The main sections of Windows Defender Firewall with Advanced Security were explored, including inbound and outbound rules, connection security rules, and the monitoring of security associations in Main Mode and Quick Mode.

---

[Back to Classes 43–44](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
