# Suricata Integration with Wazuh

## Objective

The objective of this lab is to integrate the Suricata Intrusion Detection System (IDS) with the Wazuh Security Information and Event Management (SIEM) platform to monitor network traffic, detect threats, and generate security alerts.

## Lab Environment

| Component | Version |
|----------|----------|
| Ubuntu Server | 22.04 |
| Wazuh | 4.14.6 |
| Suricata | Latest stable package |
| Kali Linux | Attack Machine |
| VMware Workstation | Hypervisor |

## Workflow

Kali Linux
↓
Network Traffic
↓
Suricata IDS
↓
eve.json
↓
Wazuh Log Collector
↓
JSON Decoder
↓
Suricata Rules
↓
Wazuh Dashboard

## Contents

- Installation
- Configuration
- Integration
- Troubleshooting
- Validation
- Screenshots
