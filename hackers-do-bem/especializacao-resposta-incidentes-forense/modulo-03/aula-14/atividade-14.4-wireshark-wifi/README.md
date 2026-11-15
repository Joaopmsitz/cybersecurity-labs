# Activity 14.4 — Wireless Network Capture Analysis with Wireshark

> **Program:** Hackers do Bem  
> **Stage:** Specialization — Incident Response and Digital Forensics  
> **Module:** 03  
> **Class:** 03  
> **Course Lesson:** 14  
> **Environment:** Windows forensic workstation  
> **Status:** Completed

## 1. Objective

Configure Wireshark to decrypt protected IEEE 802.11 wireless traffic using a pre-shared WPA password and the corresponding SSID.

The activity uses the Wireshark wireless protocol preferences to configure a decryption key.

The required key type is:

```text
wpa-pwd
```

The key string supplied by the exercise is:

```text
Induction:Coherer
```

The objective is to understand how Wireshark uses the WPA passphrase and SSID to derive the key material required to decrypt supported wireless packets.

## 2. Environment

| Item | Details |
|---|---|
| Analysis Tool | Wireshark |
| Operating System | Windows forensic workstation |
| Protocol | IEEE 802.11 |
| Wireless Security | WPA/WPA2 Personal pre-shared key mode |
| Key Type | `wpa-pwd` |
| Passphrase | `Induction` |
| SSID | `Coherer` |
| Required Key String | `Induction:Coherer` |
| Main Configuration Area | Preferences → Protocols → IEEE 802.11 |
| Evidence | Wireshark wireless decryption key configuration |

The activity uses a wireless packet capture supplied by the course.

The exact capture filename is not preserved in the supplied activity summary.

## 3. IEEE 802.11 and WPA Concepts

### IEEE 802.11

IEEE 802.11 is the family of standards used by wireless local area networks.

A wireless packet capture may contain management, control, and data frames.

When wireless security is enabled, protected data frames may require decryption before their application-layer contents can be examined.

### WPA Pre-Shared Key Mode

WPA and WPA2 Personal mode use a pre-shared password and the wireless network SSID to derive key material.

The password alone is not sufficient to derive the expected key without the correct network identifier.

The SSID is therefore an important part of the decryption configuration.

### Wireshark Wireless Decryption

Wireshark supports decryption of supported wireless captures through the IEEE 802.11 protocol preferences.

The analyst can add a key and select the appropriate key type.

For WPA Personal passphrase-based configuration, the relevant key type is:

```text
wpa-pwd
```

The expected value is formatted as:

```text
password:SSID
```

For this activity:

```text
Induction:Coherer
```

### WPA Handshake Requirement

WPA/WPA2 decryption normally requires the relevant four-way EAPOL handshake to be present in the capture.

If the required handshake packets are missing, Wireshark may be unable to derive the session keys and decrypt the protected traffic.

The existence of a configured password does not guarantee decryption if the required capture material is unavailable.

## 4. Procedure

### Step 1 — Open the Wireless Packet Capture

Wireshark was opened on the Windows forensic workstation.

The wireless capture supplied by the course was loaded.

The capture contains IEEE 802.11 traffic protected using a WPA-compatible pre-shared key configuration.

The exact capture filename was not included in the supplied summary.

### Step 2 — Open Wireshark Preferences

The following menu path was accessed:

```text
Edit → Preferences
```

Within the Preferences window, the protocol list was expanded and the following protocol was selected:

```text
Protocols → IEEE 802.11
```

This section contains the wireless protocol configuration, including decryption settings.

### Step 3 — Open the Decryption Keys Configuration

Within the IEEE 802.11 preferences, the decryption key configuration was opened using the **Edit** button next to:

```text
Decryption Keys
```

The key list allows supported key types to be added.

A new entry was created.

### Step 4 — Configure the WPA-PWD Key

The following key type was selected:

```text
wpa-pwd
```

The key field was configured using the exact string:

```text
Induction:Coherer
```

The format represents:

| Component | Value |
|---|---|
| WPA Password | `Induction` |
| SSID | `Coherer` |
| Key Type | `wpa-pwd` |
| Full Key String | `Induction:Coherer` |

The colon separates the passphrase from the SSID.

The key was added to Wireshark's decryption key list.

### Step 5 — Enable Decryption

The IEEE 802.11 preferences must have decryption enabled.

The following setting should be checked:

```text
Enable decryption
```

The changes were then applied and the preferences window closed.

Wireshark can now attempt to decrypt supported protected packets using the configured key.

The required activity screenshot documents the key configuration itself.

### Step 6 — Validate the Decryption

After configuring the key, the packet capture can be examined to verify whether protected packets are decoded.

A useful display filter for locating handshake packets is:

```text
eapol
```

The presence of the relevant EAPOL handshake is important for WPA/WPA2 Personal decryption.

If the expected packet contents are not decoded, the analyst should verify:

- Whether the correct SSID was supplied.
- Whether the passphrase is correct.
- Whether the key type is `wpa-pwd`.
- Whether decryption is enabled.
- Whether the required handshake is present.
- Whether the capture contains the complete relevant exchange.

## 5. Expected Results

The activity demonstrates the correct configuration of a WPA passphrase and SSID in Wireshark.

| Setting | Value |
|---|---|
| Protocol | IEEE 802.11 |
| Decryption Enabled | Yes |
| Key Type | `wpa-pwd` |
| Password | `Induction` |
| SSID | `Coherer` |
| Key String | `Induction:Coherer` |

With the required handshake and compatible capture data, Wireshark can attempt to decrypt supported protected wireless frames.

## 6. Technical Analysis

### Why the SSID Is Required

For WPA/WPA2 Personal mode, key derivation uses both the passphrase and SSID.

The SSID is therefore part of the input used to derive the pre-shared key material.

Using the correct password with an incorrect SSID will not produce the expected result.

### wpa-pwd Versus wpa-psk

Wireshark supports multiple wireless key types.

The key type used in this activity is:

```text
wpa-pwd
```

This format accepts the passphrase and SSID:

```text
password:SSID
```

The alternative `wpa-psk` format expects a previously derived raw pre-shared key represented in hexadecimal form.

The two formats are not interchangeable without converting the key material appropriately.

### Importance of the Four-Way Handshake

WPA/WPA2 traffic uses session-specific key material.

The handshake provides information needed to derive the keys used for protected data frames.

A capture without the required handshake may not be decryptable even when the passphrase and SSID are known.

For this reason, Wireshark's configuration must be evaluated together with the contents of the capture.

### Forensic Interpretation

Successful decryption may expose network-layer and application-layer information that was previously protected.

This can help identify:

- Internal communication.
- Protocol usage.
- Network services.
- Application activity.
- Other evidence relevant to an investigation.

The decrypted output must be correlated with the captured timestamps, endpoints, and other artifacts.

## 7. Results and Interpretation

The activity demonstrates how Wireshark can be configured to decrypt a supported WPA-protected wireless capture.

The configured entry uses:

```text
Key Type: wpa-pwd
Key: Induction:Coherer
```

The passphrase is `Induction`, and the SSID is `Coherer`.

The exercise reinforces the relationship between the wireless password, SSID, handshake material, and successful decryption.

## 8. Concepts Practiced

- Wireless network forensics
- IEEE 802.11
- WPA
- WPA2
- Pre-shared key
- SSID
- WPA passphrase
- `wpa-pwd`
- `wpa-psk`
- Wireshark preferences
- Wireless traffic decryption
- EAPOL
- Four-way handshake
- Packet capture analysis
- Decryption validation

## 9. Evidence

**Required screenshot: Print 5 — PDF page 4.**

The screenshot should display Wireshark's preferences window at:

```text
Protocols → IEEE 802.11
```

The decryption key list should show the configured entry:

```text
wpa-pwd
Induction:Coherer
```

The screenshot should make the key type and exact key string legible.

[View Class Evidence PDF](../evidences.pdf)

The required screenshot for Activity 14.4 is on page 4 of the consolidated PDF.

## References

- [Wireshark User's Guide — IEEE 802.11 WLAN Decryption Keys](https://www.wireshark.org/docs/wsug_html/)
- [Wireshark Wiki — How to Decrypt 802.11](https://wiki.wireshark.org/HowToDecrypt802.11/)

---

[Back to Module 03](../../README.md) · [Back to Specialization](../../../README.md) · [Next Activity — 14.5](../atividade-14.5-wireshark-nmap/README.md)
