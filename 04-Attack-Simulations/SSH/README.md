# SSH Authentication Failure Simulation

## Objective

The objective of this lab is to simulate an SSH authentication attack from a Kali Linux machine against an Ubuntu Server monitored by Wazuh. The lab demonstrates how failed SSH login attempts are recorded by the operating system, collected by the Wazuh agent, analyzed by the Wazuh Manager, and investigated through the Wazuh Dashboard.

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Host Operating System | Windows 11 |
| Virtualization Platform | VMware Workstation Pro |
| SIEM Platform | Wazuh 4.x |
| Target Machine | Ubuntu Server |
| Attack Machine | Kali Linux |
| Protocol | SSH |
| Default Port | 22/TCP |

---

# Lab Architecture

```
                Kali Linux
          (192.168.109.128)
                   │
                   │ SSH Authentication Attempt
                   ▼
        Ubuntu Server (SSH Service)
          (192.168.109.134)
                   │
                   ▼
        Authentication Logs (journald)
                   │
                   ▼
             Wazuh Agent
                   │
                   ▼
            Wazuh Manager
                   │
                   ▼
         Wazuh Threat Hunting
                   │
                   ▼
        Incident Investigation
```

---

# Attack Scenario

A test user named **soclab** was created on the Ubuntu Server.

The Kali Linux machine attempted to authenticate to the SSH service using incorrect passwords multiple times.

Ubuntu recorded the authentication failures.

The Wazuh agent collected these events and forwarded them to the Wazuh Manager.

Wazuh generated security alerts, which were investigated through the Threat Hunting dashboard.

---

# Attack Steps

## Step 1 – Verify SSH Service

Verified that the SSH service was running on the Ubuntu Server.

Command:

```bash
sudo systemctl status ssh
```

---

## Step 2 – Create Test User

Created a dedicated test account.

```bash
sudo adduser soclab
sudo passwd soclab
```

---

## Step 3 – Perform Failed SSH Login

From Kali Linux:

```bash
ssh soclab@192.168.109.134
```

An incorrect password was entered multiple times to generate authentication failure events.

---

## Step 4 – Verify Authentication Logs

Verified that Ubuntu recorded the failed authentication attempts.

Command:

```bash
sudo journalctl -u ssh -n 20 --no-pager
```

Observed log entries:

- authentication failure
- Failed password for soclab
- Connection closed

---

## Step 5 – Verify Wazuh Detection

Opened the Wazuh Dashboard.

Navigation:

```
Threat Hunting
```

Search:

```
rule.groups:sshd
```

Detected alert:

```
sshd: authentication failed.
```

---

# Detection Details

| Property | Value |
|----------|-------|
| Rule ID | 5760 |
| Rule Description | sshd: authentication failed. |
| Rule Level | 5 |
| Decoder | sshd |
| Log Source | journald |
| Agent | wazuhserver |

---

# Investigation Summary

The alert investigation identified:

- Source IP: **192.168.109.128**
- Username: **soclab**
- Protocol: **SSH**
- Source Port: **40682**
- Event Type: Authentication Failure
- Rule Fired: **4 Times**

The event confirms that repeated failed SSH authentication attempts were detected and processed successfully.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | Technique ID |
|---------|-----------|--------------|
| Credential Access | Password Guessing | T1110.001 |
| Lateral Movement | SSH | T1021.004 |

---

# Evidence

The following screenshots were collected during the simulation.

| Screenshot | Description |
|------------|-------------|
| ssh-service-status.png | SSH service running on Ubuntu |
| ssh-failed-login.png | Failed SSH login attempts from Kali Linux |
| auth-log-failed-login.png | Authentication failure recorded in Ubuntu logs |
| wazuh-ssh-alert.png | SSH authentication failure detected in Wazuh |
| wazuh-ssh-investigation.png | Detailed investigation of the generated alert |

---

# Learning Outcomes

This lab demonstrates:

- SSH service management
- Linux user management
- Authentication log analysis
- Wazuh log collection
- Threat Hunting
- Incident investigation
- MITRE ATT&CK mapping
- SOC monitoring workflow

---

# Conclusion

The SSH authentication failure simulation successfully demonstrated the end-to-end detection workflow within the SOC Home Lab.

Multiple failed SSH login attempts were generated from the Kali Linux attacker machine. Ubuntu recorded the authentication failures in the system logs, the Wazuh agent forwarded the events to the Wazuh Manager, and Rule **5760** was triggered. The alert was investigated using the Wazuh Threat Hunting dashboard, confirming the source IP, targeted user account, and MITRE ATT&CK techniques associated with the activity.

This exercise validates the SOC Home Lab's ability to detect, monitor, and investigate SSH authentication attacks.
