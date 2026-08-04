# Nmap Attack Simulation

## Objective

This simulation demonstrates how an attacker performs reconnaissance using Nmap and how Suricata detects the scan while Wazuh generates alerts for investigation.

---

## Lab Environment

| Component | IP Address |
|-----------|------------|
| Kali Linux (Attacker) | 192.168.109.128 |
| Ubuntu Server (Wazuh + Suricata) | 192.168.109.134 |

---

## Attack Goal

The objective is to discover open ports and running services on the target machine.

---

## Attack Command

```bash
nmap -sS -sV 192.168.109.134
```

---

## Expected Detection

The scan should generate network events that are logged by Suricata in:

- eve.json

Wazuh reads the Suricata alerts and displays them in the Wazuh Dashboard.

---

## Detection Workflow

Kali Linux
↓
Nmap Scan
↓
Ubuntu Server
↓
Suricata IDS
↓
eve.json
↓
Wazuh Manager
↓
Wazuh Dashboard
↓
Security Analyst Investigation

---

## MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Active Scanning | T1595 |

---

## Outcome

The Nmap scan successfully generated network traffic that was analyzed by Suricata and forwarded to Wazuh for centralized monitoring and alerting.
