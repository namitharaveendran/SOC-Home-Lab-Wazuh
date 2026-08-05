
# Incident Response Report – Nmap Reconnaissance Activity

## Incident Summary

A reconnaissance activity was performed from a Kali Linux machine against the Ubuntu Server hosting the Wazuh Manager and Suricata IDS. The objective was to simulate the initial phase of a cyber attack and verify that Suricata and Wazuh correctly captured and processed the generated network events.

---

## Incident Information

| Field | Value |
|-------|-------|
| Incident ID | IR-001 |
| Date | 05-Aug-2026 |
| Analyst | Namitha Raveendran |
| Attack Type | Network Reconnaissance |
| Tool Used | Nmap |
| Detection Source | Suricata IDS |
| SIEM | Wazuh |

---

## Attack Details

### Attacker Machine

- Operating System: Kali Linux
- IP Address: 192.168.109.128

### Target Machine

- Operating System: Ubuntu Server
- IP Address: 192.168.109.134

---

## Attack Command

```bash
nmap -sS -sV 192.168.109.134
```

### Purpose

The attacker performed a TCP SYN scan to identify open ports and running services on the target server.

---

## Detection

Suricata generated alerts that were forwarded to the Wazuh Manager.

Detected Rule:

```
Rule ID: 86601
```

Description:

```
Suricata: Alert – ET POLICY Possible Kali Linux hostname in DHCP Request Packet
```

Severity:

```
Level 3
```

---

## Investigation

The alert was investigated using the Wazuh Threat Hunting module.

Observed Details:

- Rule ID: 86601
- Event Type: Alert
- Protocol: UDP
- Source Port: 68
- Destination Port: 67
- Source IP: 0.0.0.0
- Destination IP: 255.255.255.255
- Decoder: JSON
- Log Source: /var/log/suricata/eve.json

---

## Analysis

Although the attack simulation used Nmap, the generated alert corresponds to a DHCP request containing the Kali Linux hostname.

The alert confirms that:

- Suricata successfully inspected the network traffic.
- Events were written to eve.json.
- Wazuh successfully parsed the JSON logs.
- The alert appeared in the Wazuh Dashboard.
- The event could be investigated using Threat Hunting.

This validates the integration between Suricata and Wazuh.

---

## Impact Assessment

Current Risk Level:

Low

Reason:

The detected event is informational and indicates the presence of a Kali Linux host rather than a confirmed attack. However, identifying systems commonly used for penetration testing can provide valuable security context.

---

## Response Actions

- Verified Suricata service status.
- Verified Wazuh Manager status.
- Confirmed eve.json logging.
- Confirmed alert ingestion by Wazuh.
- Investigated the event using Threat Hunting.
- Documented the incident.

---

## Lessons Learned

This exercise demonstrated the complete SOC monitoring workflow:

1. Attack simulation using Nmap.
2. Network inspection by Suricata.
3. Event logging in eve.json.
4. Log collection by Wazuh.
5. Alert visualization in the Wazuh Dashboard.
6. Alert investigation through Threat Hunting.

---

## MITRE ATT&CK Mapping

| Technique | ID |
|-----------|----|
| Active Scanning | T1595 |

---

## Evidence

### Screenshots

- screenshots/nmap-command.png
- screenshots/eve-json-nmap-alert.png
- screenshots/wazuh-dashboard-nmap-alert.png
- screenshots/investigation.png

---

## Conclusion

The objective of the attack simulation was successfully achieved. Network events generated during reconnaissance were captured by Suricata, processed by Wazuh, and investigated using the Threat Hunting interface. This validates the functionality of the SOC Home Lab and demonstrates the end-to-end detection and investigation workflow.
