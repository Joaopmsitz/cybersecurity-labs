# Activity 11.03 — MAC Cloning on Kali Linux

## Objective

Explore how to change the MAC address of a network interface on Kali Linux by temporarily cloning the MAC address of the `docker0` interface and then restoring its original MAC address.

This activity demonstrates how a network interface's hardware address can be changed in software and how to verify the change using Linux networking tools.

## Environment

- **Operating system:** Kali GNU/Linux
- **Interface under examination:** `docker0`
- **Tools:** `ip link` and `ifconfig`
- **Original `docker0` MAC address:** `02:42:4c:36:59:3d`
- **MAC address used for testing:** `08:00:27:8b:c0:05`

## 1. Accessing Kali Linux

The Kali Linux machine was accessed, and the Terminal was opened.

Administrative privileges were obtained using:

```bash
sudo -i
```

## 2. Displaying Network Interfaces

The available interfaces were checked using:

```bash
ip link show
```

The output was:

```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 12:4d:70:f0:ab:8b brd ff:ff:ff:ff:ff:ff
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000
    link/ether 02:42:4c:36:59:3d brd ff:ff:ff:ff:ff:ff
```

The `docker0` interface was configured with the following MAC address:

```text
02:42:4c:36:59:3d
```

This address was recorded so it could be restored at the end of the activity.

### Observed Interfaces

- **`lo`:** Loopback interface.
- **`eth0`:** Main network interface.
- **`docker0`:** Virtual bridge used by Docker.

## 3. Displaying Interfaces with ifconfig

The following command was also used:

```bash
ifconfig
```

The output confirmed the network interface information, including the `docker0` MAC address:

```text
docker0: ...
          ether 02:42:4c:36:59:3d
```

The original MAC address of the `docker0` interface was retained as a reference for the restoration step.

> **Important:** The original MAC address may vary depending on the machine or environment. In this lab, the observed original address was `02:42:4c:36:59:3d`.

## 4. Disabling the docker0 Interface

Before changing the MAC address, the interface was disabled:

```bash
ip link set docker0 down
```

Disabling the interface allows the address change to be performed while the interface is administratively down.

## 5. Changing the MAC Address

A new MAC address was assigned to the `docker0` interface:

```bash
ip link set dev docker0 address 08:00:27:8b:c0:05
```

At this point, the interface's MAC address was temporarily changed to:

```text
08:00:27:8b:c0:05
```

This technique is known as **MAC cloning** or **MAC spoofing**, because it allows an interface to use a MAC address different from the one originally configured.

## 6. Re-enabling the Interface

After the change, the interface was enabled again:

```bash
ip link set docker0 up
```

## 7. Verifying the New MAC Address

The change was verified using:

```bash
ip link show
```

The `docker0` interface then displayed:

```text
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default
    link/ether 08:00:27:8b:c0:05 brd ff:ff:ff:ff:ff:ff
```

The displayed MAC address changed from:

```text
02:42:4c:36:59:3d
```

to:

```text
08:00:27:8b:c0:05
```

This confirms that the MAC address change was applied to the interface.

## 8. Restoring the Original MAC Address

After completing the test, the original MAC address was restored.

First, the interface was disabled:

```bash
ip link set docker0 down
```

Next, the original MAC address recorded at the beginning of the activity was assigned again:

```bash
ip link set dev docker0 address 02:42:4c:36:59:3d
```

Finally, the interface was enabled again:

```bash
ip link set docker0 up
```

### Evidence — Step 8

**Caption to include before the screenshot:**

> Screenshot of Activity 11.03: restoration of the original MAC address of the `docker0` interface after the MAC cloning test, using the address `02:42:4c:36:59:3d` again.

[View Evidence — Classes 41–42](../evidencias.pdf)

> **Observation:** If the original MAC address differs on another machine, use the value recorded before the change rather than assuming it is `02:42:4c:36:59:3d`.

## 9. Verifying the Restoration

After restoring the address, the interface configuration was checked again:

```bash
ip link show
```

The `docker0` interface should once again display the original MAC address recorded at the beginning of the activity:

```text
link/ether 02:42:4c:36:59:3d
```

## 10. Closing the Activity

After confirming that the original MAC address had been restored, the Terminal was closed.

## Key Concepts

- **MAC address:** An identifier used at the link layer to identify a network interface.
- **MAC cloning:** Changing the MAC address presented by an interface to another address.
- **`ip link`:** A Linux utility used to display and modify network interfaces.
- **`docker0`:** A virtual bridge created by Docker for communication between containers.
- **MAC spoofing:** A technique for changing the MAC address used by a network interface.

## Activity Workflow

```text
Check the original MAC address
        ↓
Disable docker0
        ↓
Change the MAC address
        ↓
Re-enable the interface
        ↓
Verify the change
        ↓
Restore the original MAC address
        ↓
Verify the restoration
```

## Result

The MAC address of the `docker0` interface was temporarily changed to `08:00:27:8b:c0:05`, and the change was confirmed using `ip link show`. Finally, the original MAC address, `02:42:4c:36:59:3d`, was restored.

---

[Back to Classes 41–42](../) · [Back to Module 11](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
