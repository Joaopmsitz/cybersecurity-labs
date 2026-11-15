# Activity 7.3 - Using Threat Intelligence Sources

## Overview

This activity enriches Zeek with external threat intelligence indicators. The practical exercise uses domain indicators associated with the Pegasus spyware investigations and demonstrates how to add IP indicators from a separate feed.

## Objectives

- Locate a threat intelligence feed.
- Identify Pegasus-related domain indicators.
- Add domain and IP indicators to Zeek intelligence files.
- Configure Zeek to load multiple intelligence sources.

## Threat Intelligence Sources

| Source | Description |
|---|---|
| Critical Path Security - Zeek Intelligence Feeds | Repository of Zeek-formatted threat intelligence feeds |
| Amnesty NSO Domains | Domain indicators associated with the Pegasus-related investigations |
| Compromised IPs | IP address indicators provided through the feed repository |

## Procedure

### 1. Locate the Pegasus Domain Feed

Open the repository:

- [Critical Path Security - Zeek Intelligence Feeds](https://github.com/CriticalPathSecurity/Zeek-Intelligence-Feeds)

Locate `Amnesty_NSO_Domains.intel` in the Sources section and follow its List URL to the associated Amnesty International investigation material.

Open `domains.txt` and inspect the listed domains.

### 2. Add Domain Indicators

Configure the terminal prompt as required by the course before capturing terminal evidence:

```bash
export PS1="$(echo "\d \t $PS1"|sed -e 's/\\\u/meunome/g')"
```

Edit the Zeek intelligence file:

```bash
sudo nano /opt/zeek/intel/zeek_intel.txt
```

The exercise uses the first domain indicators from the provided list. The sample rows below reproduce the course examples:

```text
#fieldsindicatorindicator_type
123tramites.comIntel::DOMAIN
14-tracking.comIntel::DOMAIN
1minto-start.comIntel::DOMAIN
24-7clinic.comIntel::DOMAIN
301-redirecting.comIntel::DOMAIN
```

Separate fields with literal TAB characters.

### 3. Add IP Indicators

The repository also provides the `compromised-ips.intel` feed.

Create a second intelligence file:

```bash
sudo nano /opt/zeek/intel/zeek_intel2.txt
```

The following are example rows from the practical material:

```text
#fieldsindicatorindicator_type
101.43.21.125Intel::ADDR
102.128.78.76Intel::ADDR
102.223.74.186Intel::ADDR
103.114.107.163Intel::ADDR
103.116.52.103Intel::ADDR
103.125.161.93Intel::ADDR
```

Separate fields with literal TAB characters.

### 4. Configure Zeek to Load Both Files

Edit the local configuration:

```bash
sudo nano /opt/zeek/share/zeek/site/local.zeek
```

Configure both intelligence files:

```zeek
# Enable the Zeek Intelligence Framework
@load frameworks/intel/seen

redef Intel::read_files += {
    "/opt/zeek/intel/zeek_intel.txt",
    "/opt/zeek/intel/zeek_intel2.txt",
};
```

Apply the configuration:

```bash
sudo /opt/zeek/bin/zeekctl stop
sudo /opt/zeek/bin/zeekctl deploy
```

## Expected Result

The Zeek Intelligence Framework is configured to load both domain and IP indicators from the two local intelligence files.

## Evidence

**Required screenshot: Step 4 - Print 8, PDF page 3.**

The screenshot must show `zeek_intel.txt` populated with the initial Pegasus-related domain indicators, with fields separated by literal TAB characters.

- [View consolidated evidence](../evidences.pdf)

## Technical Notes

- Zeek intelligence files use a `#fields` header.
- The `indicator_type` field determines how Zeek interprets each indicator.
- `Intel::DOMAIN` is used for domain names.
- `Intel::ADDR` is used for IP addresses.
- Threat intelligence feeds should be reviewed for freshness and context before being used in production.
- The sample indicators are included to document the training exercise, not to assert that each domain or address remains malicious today.

## References

- [Critical Path Security - Zeek Intelligence Feeds](https://github.com/CriticalPathSecurity/Zeek-Intelligence-Feeds)
- [Amnesty International - NSO Investigation](https://github.com/AmnestyTech/investigations/tree/master/2021-07-18_nso)
- [Zeek - Intelligence Framework](https://docs.zeek.org/en/current/frameworks/intel.html)

## Navigation

- [Class 07](../README.md)
- [Previous Activity - 7.2](../atividade-7.2-analisando-correspondencias/README.md)
- [Next Activity - 7.4](../atividade-7.4-threat-hunting-zeek/README.md)
