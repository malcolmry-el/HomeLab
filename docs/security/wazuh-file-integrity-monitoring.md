# Wazuh File Integrity Monitoring (FIM)

## Objective

Configure Wazuh File Integrity Monitoring (FIM) to monitor critical Linux system files in real time and generate alerts when files are created, modified, or deleted.

---

## Environment

| Component | Version |
|-----------|---------|
| Ubuntu Server | 26.04 |
| Wazuh Manager | Docker (Single Node) |
| Wazuh Agent | Ubuntu Server |
| Monitoring Mode | Realtime |

---

## Configuration

Updated the Wazuh agent configuration:

```xml
<directories realtime="yes" check_all="yes">/etc,/usr/bin,/usr/sbin</directories>
<directories realtime="yes" check_all="yes">/bin,/sbin,/boot</directories>
```

Restarted the Wazuh agent:

```bash
sudo systemctl restart wazuh-agent
```

---

## Validation

Created a test file:

```bash
sudo touch /etc/fim-test2.txt
echo "hello" | sudo tee -a /etc/fim-test2.txt
```

Wazuh immediately generated:

- Rule 554 — File Added
- Rule 550 — Integrity Checksum Changed
- Rule 553 — File Deleted

Additional testing confirmed realtime monitoring of changes to protected files under `/etc`.

---

## Security Value

File Integrity Monitoring helps detect:

- Unauthorized file modifications
- Malware persistence
- Privilege escalation
- Configuration drift
- Insider threats

Critical system files monitored include:

- /etc/passwd
- /etc/shadow
- /etc/group
- /etc/gshadow
- System binaries
- Boot files

---

## Lessons Learned

Initially, File Integrity Monitoring was configured for scheduled scans every 12 hours.

Enabling:

```xml
realtime="yes"
```

allowed Wazuh to immediately detect filesystem changes without waiting for the next scheduled scan.

This configuration provides significantly better visibility into endpoint activity.

---

## Skills Demonstrated

- Linux Administration
- Wazuh SIEM
- Endpoint Detection
- File Integrity Monitoring (FIM)
- Security Monitoring
- Threat Detection
- SOC Operations
