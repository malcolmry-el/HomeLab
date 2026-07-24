# 🏠 HomeLab

A self-hosted enterprise-style homelab built to develop practical skills in networking, Linux administration, Docker, monitoring, reverse proxying, and cybersecurity.

This repository documents the infrastructure, configurations, and services running in my lab.

---

## 🖥️ Network Architecture

![Network Architecture](diagrams/network-overview.png)

---
## 🚀 Infrastructure

- Ubuntu Server
- Docker & Docker Compose
- Portainer
- Homepage Dashboard
- Nginx Proxy Manager
- Git & GitHub

---

## 📊 Monitoring Stack

### Components

- Grafana
- Prometheus
- Node Exporter
- cAdvisor

----

## Security Monitoring

✅ Wazuh SIEM

- Endpoint Monitoring
- Authentication Monitoring
- File Integrity Monitoring (Realtime)
- Rootcheck
- Threat Hunting
- MITRE ATT&CK Mapping
- Vulnerability Detection (In Progress)

### Current Security Coverage

- Ubuntu Server
- pfSense Firewall
- Snort IDS Alerts
- Linux Authentication Logs
- Docker Host Monitoring

----

#### ⭐ Highlights

- Custom Grafana dashboard built from scratch
- Prometheus monitoring stack
- Docker container monitoring with cAdvisor
- Host monitoring with Node Exporter
- Reverse proxy using Nginx Proxy Manager
- Docker management with Portainer
- Service availability monitoring with Uptime Kuma

----

### Infrastructure Dashboard

The Grafana dashboard provides:

- Docker container monitoring
- CPU usage
- Memory usage
- Disk utilization
- Network activity
- System uptime
- Container CPU usage
- Container memory usage
- Historical CPU trends
- Historical memory trends

Dashboard JSON:

docker/monitoring/grafana/dashboards/homelab-infrastructure.json
----

## 🌐 Network

Network components include:

- pfSense Firewall
- TP-Link Omada Managed Switch
- VLAN segmentation
- Reverse Proxy
- Static DHCP Reservations

----

## 📁 Repository Structure

```text
docker/
├── homepage/
├── monitoring/
├── nginx-proxy-manager/

docs/
├── diagrams/
├── homepage/
├── monitoring/
└── networking/
```

----

## 📸 Dashboard

HomePage

![Homepage](docs/images/homepage-dashboard.png)

----

## 🎯 Goals

This homelab is designed to gain hands-on experience with:

- Linux Administration
- Docker
- Networking
- Monitoring
- Reverse Proxy
- Infrastructure Documentation
- Cybersecurity
- Automation

----

## 🔨 Planned Services

- Wazuh SIEM
- Authentik SSO
- CrowdSec
- Vaultwarden
- Immich
- Jellyfin
- Ansible

----

## 📚 Documentation

Each service has its own documentation covering:

- Installation
- Configuration
- Networking
- Troubleshooting
- Maintenance

---

## 🛠️ Technologies

- Ubuntu Server
- Docker
- Docker Compose
- Grafana
- Prometheus
- Node Exporter
- Uptime Kuma
- Homepage
- Portainer
- Nginx Proxy Manager
- pfSense
- Git
- GitHub

---

## 📈 Project Status

Current Phase:

✅ Infrastructure Complete

✅ Docker Monitoring Stack

✅ Custom Grafana Dashboard

✅ Security Stack (Wazuh)

🔄 Documentation Improvements

⏳ Identity Management (Authentik)

⏳ Automation
