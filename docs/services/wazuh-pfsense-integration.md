# pfSense Integration with Wazuh

## Overview

This document describes how I integrated my pfSense firewall with my Docker-based Wazuh deployment using Ubuntu Server as a syslog relay.

The project documents the troubleshooting process, configuration changes, validation steps, and final working solution.

---
# Environment

## Hardware

| Device | Purpose |
|---------|----------|
| Lenovo Laptop | Ubuntu Server |
| pfSense Mini PC | Router / Firewall |
| Gaming PC | Windows Endpoint |

## Software

| Software | Version |
|-----------|----------|
| Ubuntu Server | 26.04 |
| Docker | Compose |
| Wazuh | 4.14.6 |
| pfSense | CE |

## Network

| Device | Address |
|----------|----------|
| pfSense | 192.168.50.1 |
| Ubuntu Server | 192.168.50.2 |
| Docker Bridge | 172.23.0.0/16 |

---
# Goal

Collect firewall logs from pfSense and display them inside Wazuh with full parsing and rule matching.

Desired flow:

pfSense
↓
Ubuntu Server
↓
rsyslog
↓
Docker
↓
Wazuh Manager
↓
Dashboard Alerts

---
# Initial Problem

pfSense was successfully sending syslog messages.

The messages appeared inside Wazuh's archives.

However, Wazuh failed to decode them.

Every event appeared similar to:

```
decoder: {}
```

instead of using the built-in pfSense decoder.

No firewall alerts were generated.

---
# Root Cause

The syslog messages arriving from pfSense looked similar to:

```

Jul 21 13:43:05 filterlog[8563]:

```

Wazuh interpreted:

```

hostname = filterlog[8563]:
program_name = (empty)

```

The built-in pfSense decoder expects:

```

program_name = filterlog

```

Since the program name was missing, the decoder never matched.

---
# Troubleshooting Process

## Step 1

Verified pfSense was sending syslog.

Configured:

Status → System Logs → Settings

Remote Logging

Destination:

192.168.50.2

Port:

514

Protocol:

UDP

---

## Step 2

Verified Ubuntu was receiving packets.

Command:

```bash
sudo tcpdump -ni any udp port 514
```

Observed:

```
192.168.50.1
↓

192.168.50.2
```

Confirmed:

Ubuntu successfully received firewall logs.

---

## Step 3

Verified rsyslog.

Enabled UDP listener.

Configuration:

```conf
module(load="imudp")
input(type="imudp" port="514")
```

---

## Step 4

Created forwarding rule.

```conf
if ($fromhost-ip == '192.168.50.1') then {
    action(
        type="omfwd"
        target="127.0.0.1"
        port="5514"
        protocol="udp"
    )
    stop
}
```

---

## Step 5

Changed Docker port mapping.

Original:

514 → 514

New:

5514 → 514

This prevented rsyslog and Docker from attempting to bind to the same UDP port.

---

## Step 6

Verified forwarding.

tcpdump confirmed:

192.168.50.1
↓

Ubuntu
↓

172.23.0.2

Packets reached the Wazuh container.

---

## Step 7

Wazuh rejected packets.

Error:

Message from 172.23.0.1 not allowed

Cause:

Docker bridge IP not included in allowed-ips.

---

## Step 8

Updated Wazuh configuration.

Changed:

```xml
<allowed-ips>192.168.50.0/24</allowed-ips>
```

to

```xml
<allowed-ips>172.23.0.0/16</allowed-ips>
```

Restarted Wazuh Manager.

---
# Validation

Verified:

✓ Packets reached Ubuntu.

✓ Packets reached Docker.
# Final Result


---
✓ Wazuh accepted packets.

✓ Wazuh decoded filterlog.

✓ Wazuh generated firewall alerts.

Verified in:

Threat Hunting

Example rule:

87702

Description:

Multiple pfSense firewall blocks events from same source.

---

