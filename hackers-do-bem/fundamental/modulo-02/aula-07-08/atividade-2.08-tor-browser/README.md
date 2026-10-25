# Activity 2.08 — Exploring Tor Browser on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 02  
> **Class:** 07–08  
> **Environment:** Kali Linux virtual lab  
> **Status:** Completed

## Objective

Configure and use Tor Browser on Kali Linux to observe how a connection through the Tor network can present a different public IP address from a conventional browser connection.

The activity also examines information associated with the IP addresses reported by an external lookup service, comparing access through Tor Browser with access through a conventional browser.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Browser:** Tor Browser
- **Conventional browser:** Firefox
- **Launcher:** `torbrowser-launcher`
- **Network:** Tor
- **IP lookup service:** WhatIsMyIPAddress

## Procedure

### 1. Launch Tor Browser

Tor Browser was started from the terminal using:

```bash
torbrowser-launcher
```

During the first launch, the launcher downloaded and prepared the browser. The following output was observed:

```text
Lançador do Navegador Tor
By Micah Lee & Tor Project, licensed under MIT
versão 0.3.7
https://gitlab.torproject.org/tpo/applications/torbrowser-launcher/
Criando o diretório inicial do GnuPG /home/aluno/.local/share/torbrowser/gnupg_homedir
Downloading Tor Browser for the first time.
Baixando https://aus1.torproject.org/torbrowser/update_3/release/Linux_x86_64-gcc3/x/ALL
MESA: error: ZINK: failed to choose pdev
glx: failed to create drisw screen
Versão mais recente: 13.5.6
Baixando https://dist.torproject.org/torbrowser/13.5.6/tor-browser-linux-x86_64-13.5.6.tar.xz.asc
Baixando https://dist.torproject.org/torbrowser/13.5.6/tor-browser-linux-x86_64-13.5.6.tar.xz
Verificando Assinatura
Downloading latest Tor Browser signing key...
Key imported successfully
Extraindo tor-browser-linux-x86_64-13.5.6.tar.xz
Rodando /home/aluno/.local/share/torbrowser/tbb/x86_64/tor-browser/start-tor-browser.desktop
Launching './Browser/start-tor-browser --detach'...
```

The process performed the following actions:

- Created the directory used by the launcher.
- Checked the available Tor Browser version.
- Downloaded the browser package.
- Downloaded the signing key used to verify the package.
- Verified the package signature.
- Extracted the browser archive.
- Started Tor Browser.

The MESA/ZINK messages appeared during graphical initialization. They did not prevent the activity from continuing.

The version reported during this laboratory run was **13.5.6**. This records the version observed at the time of the exercise, not necessarily the current release.

### 2. Establish a Tor Connection

After Tor Browser opened, the **Connect** option was used to establish a connection to the Tor network.

When a direct connection could not be established normally, the laboratory procedure allowed the use of **Try a bridge**.

Once connected, the browser routed its traffic through the Tor network before reaching the destination.

### 3. Browse the Web Through Tor Browser

With Tor Browser connected to the Tor network, the following website was accessed:

```text
https://duckduckgo.com/
```

The page was used to confirm that browsing through Tor was working.

A new tab was then opened to check the externally observed IP address:

```text
https://whatismyipaddress.com/
```

The privacy prompt displayed by the website was accepted to view the available information.

### 4. Check the IP Address Through Tor

The lookup service displayed an IPv4 address and information associated with the exit node used during the laboratory session.

The observed output was:

```text
IPv6: ? 2a0b:f4c0:16c:16::1

IPv4: ? 185.220.100.240

Your location may be exposed!
Hide My IP Address Now

Show Complete IP Details

My IP Information:

ISP: Stiftung Erneuerbare Freiheit

Services: Tor Exit Node

City: Frankfurt am Main

Region: Hessen

Country: Germany
```

The result identified the address as belonging to a **Tor Exit Node**, indicating that the connection reached the public Internet through a Tor exit relay.

The location reported by the lookup service corresponds to the location associated with the observed exit-node IP address. It does not necessarily represent the user's actual physical location.

### 5. Compare with a Conventional Connection

To compare the results, the same lookup service was accessed through the conventional Firefox browser, outside Tor Browser.

The observed output was:

```text
IPv4: 107.22.123.86

IPv6: Not detected

Your location may be exposed!
Hide My IP Address Now

Show Complete IP Details

My IP Information:

ISP: Amazon.com Inc.

City: Ashburn

Region: Virginia

Country: United States
```

The results showed different IP addresses for the two browser connections.

#### Observed Comparison

| Connection | IPv4 Address Observed | Information Reported by the Service |
|---|---|---|
| Tor Browser | `185.220.100.240` | Tor Exit Node / Frankfurt am Main, Germany |
| Conventional Firefox | `107.22.123.86` | Amazon.com Inc. / Ashburn, Virginia, United States |

**Historical-data note:** These addresses and geographic details are the results recorded during this laboratory exercise. They should not be interpreted as current IP addresses or as definitive evidence of the user's physical location or Internet provider.

The conventional browser result was associated with Amazon's network. This observation alone does not establish why that address was used; the surrounding virtualized or network environment can affect the externally observed IP address.

### 6. Understand How Tor Relates to the Results

In a conventional connection, a destination website generally observes the public IP address used by the client connection.

With Tor Browser, traffic is forwarded through the Tor network using multiple relays. When traffic reaches a public Internet destination, the destination generally observes the IP address of the Tor exit relay rather than the client's original public IP address.

The activity demonstrated this difference through an external IP lookup service.

However, Tor does not automatically make every activity anonymous or eliminate every possibility of identification. Privacy depends on how the browser, accounts, applications, and destination services are used. Tor also does not guarantee protection against all forms of tracking or information disclosure.

### 7. Concepts Practiced

#### Tor Network

Tor is a network designed to improve communication privacy by routing traffic through a sequence of relays.

#### Tor Browser

Tor Browser is a browser configured to use the Tor network and reduce certain forms of tracking and exposure of the user's network origin.

#### Tor Exit Node

A Tor exit node is the relay through which traffic leaves the Tor network and reaches the conventional Internet.

The destination service can observe the exit node's IP address rather than the original public IP address used by the client.

#### Public IP Address

A public IP address is used to identify the network endpoint from which an Internet connection appears to originate.

The comparison in this activity demonstrated that the address observed by an external service can differ depending on the connection path.

#### Internet Privacy

The activity provided a practical demonstration of how different connection methods affect the network information visible to external services.

## Commands Used

The terminal command used to start the browser was:

```bash
torbrowser-launcher
```

All other steps were performed through the Tor Browser and Firefox graphical interfaces.

The external IP lookup service was accessed at:

```text
https://whatismyipaddress.com/
```

## Interpreting the Results

The activity demonstrated how Tor Browser can change the IP address observed by an external website.

During the Tor Browser session, the lookup service reported:

```text
IPv4: ? 185.220.100.240

Services: Tor Exit Node

City: Frankfurt am Main

Region: Hessen

Country: Germany
```

During the conventional Firefox session, the service reported:

```text
IPv4: 107.22.123.86

IPv6: Not detected

ISP: Amazon.com Inc.

City: Ashburn

Region: Virginia

Country: United States
```

The comparison showed that the two connections presented different IPv4 addresses and different network-provider and geographic information.

The observations support the following conclusions:

- Tor Browser successfully connected through a Tor exit node during the recorded test.
- The external lookup service reported an IP address associated with a Tor exit node.
- The conventional Firefox connection presented a different public IP address.
- The geographic information returned by the service described the network address, not necessarily the physical location of the user.

These are observations from the specific laboratory run, not guarantees about future connection behavior.

## Result

The activity demonstrated how to:

- Install and launch Tor Browser through `torbrowser-launcher`.
- Establish a connection to the Tor network.
- Browse a website through Tor Browser.
- Query the IP address observed by an external service.
- Identify a Tor exit node in the returned information.
- Compare the IP address reported through Tor Browser with a conventional Firefox connection.
- Understand the role of Tor exit nodes and their effect on the IP address visible to destination services.

The main observation was the difference between the IP addresses reported for Tor Browser and conventional Firefox during the laboratory session.

## Concepts Practiced

- Tor network
- Tor Browser
- Tor relays and exit nodes
- Public IP addresses
- IP lookup services
- Network privacy
- Anonymous browsing concepts
- Virtualized network environments
- Interpretation of IP geolocation information
- Privacy limitations and operational awareness

## Evidence

The activity evidence is included in the PDF for Classes 07–08.

The screenshot recorded for the activity corresponds to **Step 7**, as specified in the laboratory instructions.

[View Evidence — Classes 07–08](../evidencia.pdf)

---

[Back to Classes 07–08](../) · [Back to Module 02](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
