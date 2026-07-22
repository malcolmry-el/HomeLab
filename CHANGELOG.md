# Changelog

All notable changes to this homelab are documented in this file.

The project follows an incremental approach where infrastructure is built, tested, documented, and expanded over time.

---

# [2026-07-17] - Ubuntu Server Deployment

## Added

- Installed Ubuntu Server 26.04 LTS.
- Configured OpenSSH Server for remote administration.
- Disabled system sleep to allow headless operation.
- Configured static DHCP reservation.
- Updated operating system packages.
- Configured hostname.
- Enabled automatic network connectivity after reboot.

## Hardware

- Lenovo laptop repurposed as dedicated home server.
- Ethernet connected to managed switch.

## Validation

- Successfully connected using SSH.
- Verified remote reboot functionality.
- Confirmed server accessible without local monitor.

---

# [2026-07-17] - Docker Platform

## Added

- Installed Docker Engine.
- Installed Docker Compose.
- Verified Docker networking.
- Configured Docker service to start automatically.

## Validation

- Successfully deployed test containers.
- Verified Docker networking.
- Confirmed persistent storage functionality.

---

# [2026-07-18] - GitHub Repository

## Added

Created GitHub repository:

HomeLab

Repository structure includes:

- README
- assets
- diagrams
- docker
- docs
- scripts
- backups

Configured Git credentials.

Generated SSH keys.

Configured GitHub authentication.

Successfully pushed initial repository.

---

# [2026-07-18] - Homepage Dashboard

## Added

Installed Homepage dashboard.

Configured:

- Infrastructure section
- Service cards
- Weather widget
- Docker integration

## Fixed

Resolved:

- Homepage configuration errors.
- Invalid OpenWeather API key.
- Host validation issue.

---

# [2026-07-18] - Portainer

## Added

Installed Portainer Community Edition.

Configured Docker management dashboard.

Verified:

- Container management
- Image management
- Volume management
- Network management

---

# [2026-07-18] - Uptime Kuma

## Added

Installed Uptime Kuma.

Configured monitoring for:

- Ubuntu Server
- Docker services

Validated monitoring and notifications.

---

# [2026-07-19] - Reverse Proxy

## Added

Installed Nginx Proxy Manager.

Configured:

- Reverse proxy service
- SSL support
- Dashboard access

---

# [2026-07-19] - Monitoring Stack

## Added

Installed:

- Prometheus
- Node Exporter
- cAdvisor

Configured Prometheus scraping.

Created Grafana data source.

Built initial dashboards.

## Fixed

Resolved:

- cAdvisor metrics
- Docker metrics
- Network throughput calculations

---

# [2026-07-20] - Wazuh Deployment

## Added

Installed Docker-based Wazuh stack.

Components:

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Indexer

Configured:

- Docker networking
- Persistent storage
- Dashboard authentication

Verified successful deployment.

---

# [2026-07-20] - Endpoint Monitoring

## Added

Connected Ubuntu server as Wazuh agent.

Verified:

- Syscheck
- Rootcheck
- Vulnerability detection
- Inventory collection

---

# [2026-07-21] - pfSense Integration

## Added

Configured pfSense remote syslog.

Configured Ubuntu rsyslog relay.

Integrated firewall logging into Wazuh.

Enabled:

- Firewall event parsing
- Correlation rules
- Dashboard visibility

## Changed

Modified Docker networking.

Previous:

Host UDP 514 → Container UDP 514

Updated:

Host UDP 5514 → Container UDP 514

Configured rsyslog forwarding.

Updated Wazuh remote listener configuration.

Allowed Docker bridge network.

## Troubleshooting

Investigated:

- Missing decoder
- Empty program_name
- filterlog parsing
- Docker networking
- UDP forwarding
- Wazuh remote listener
- Allowed IP configuration
- Packet forwarding
- Syslog normalization

Validated each network hop using tcpdump.

Confirmed:

pfSense
↓

Ubuntu

↓

rsyslog

↓

Docker

↓

Wazuh

↓

Dashboard

## Fixed

Resolved issue where pfSense logs arrived but failed to decode.

Root cause:

The original syslog format caused Wazuh to interpret:

hostname = filterlog[PID]

instead of:

program_name = filterlog

Implemented rsyslog relay to normalize syslog headers.

Verified:

- Decoder "pf"
- Rule 87701
- Rule 87702
- Dashboard alerts

---

## 2026-07-22

### Fixed
- Resolved Homepage → Wazuh reverse proxy issue.
- Corrected Homepage configuration to use the active Docker bind mount.
- Fixed Wazuh dashboard access through Nginx Proxy Manager.
- Documented Docker bind mount troubleshooting process.
## Current Status

Infrastructure

✅ Ubuntu Server

✅ Docker

✅ Docker Compose

✅ GitHub

Services

✅ Homepage

✅ Portainer

✅ Uptime Kuma

✅ Nginx Proxy Manager

Monitoring

✅ Prometheus

✅ Node Exporter

✅ cAdvisor

Security

✅ Wazuh

✅ pfSense Firewall Integration

Networking

✅ SSH

✅ Docker Networks

✅ Reverse Proxy

Documentation

✅ GitHub Repository

✅ Architecture Diagrams

✅ Service Documentation

---

# Next Phase

Planned work:

- Deploy Wazuh Windows Agent
- Deploy Wazuh Linux Agents
- Install Suricata on pfSense
- Integrate Suricata alerts into Wazuh
- Create custom Wazuh dashboards
- Build Grafana security dashboards
- Configure alert notifications
- Harden Ubuntu Server
- Add automated backups
- Implement log retention policies
