# Incident Report – SSH Authentication Failure

## Incident Summary

| Field | Value |
|------|------|
| Incident ID | SSH-001 |
| Incident Type | SSH Authentication Failure |
| Severity | Medium |
| Detection Source | Wazuh SIEM |
| Rule ID | 5760 |
| Rule Description | sshd: authentication failed |
| Date | 05 August 2026 |
| Status | Closed |

---

# Executive Summary

During this simulation, multiple failed SSH authentication attempts were generated from the Kali Linux attacker machine against the Ubuntu Server. The failed login attempts were recorded by the SSH daemon (`sshd`) and collected by the Wazuh agent through the system journal (`journald`).

The Wazuh Manager analyzed the events and generated Rule **5760**, indicating an SSH authentication failure. The alerts were successfully investigated using the Wazuh Threat Hunting dashboard.

---

# Lab Environment

| Component | Value |
|----------|------|
| SIEM | Wazuh 4.x |
| Target | Ubuntu Server |
| Attacker | Kali Linux |
| Protocol | SSH |
| Port | 22/TCP |

---

# Incident Timeline

| Time | Event |
|------|-------|
| SSH service verified | SSH service confirmed active |
| User created | Test user **soclab** created |
| Attack started | Failed SSH login attempts from Kali Linux |
| Authentication failed | Ubuntu logged failed password events |
| Wazuh Detection | Rule 5760 triggered |
| Investigation | Alert analyzed in Threat Hunting |
| Incident Closed | Attack confirmed as simulated |

---

# Attack Details

## Source Information

| Field | Value |
|------|------|
| Source IP | **192.168.109.128** |
| Username | **soclab** |
| Source Port | **40682** |
| Protocol | SSH |

---

## Target Information

| Field | Value |
|------|------|
| Hostname | wazuhserver |
| Destination Port | 22 |
| Operating System | Ubuntu Server |

---

# Detection Details

| Property | Value |
|---------|------|
| Rule ID | 5760 |
| Rule Level | 5 |
| Decoder | sshd |
| Log Source | journald |
| Fired Times | 4 |

---

# Alert Analysis

The Wazuh alert identified repeated SSH authentication failures.

Important observations include:

- Multiple failed password attempts.
- Authentication targeted the user **soclab**.
- Attack originated from the Kali Linux machine.
- Ubuntu recorded the failures in the SSH service logs.
- Wazuh successfully parsed and correlated the events.

---

# Evidence Collected

## 1. SSH Service Verification

The SSH service was confirmed to be running before the simulation.

**Evidence**

```
Active: active (running)
```

Screenshot:

```
screenshots/ssh-service-status.png
```

---

## 2. Failed SSH Login Attempts

The attacker attempted to authenticate using incorrect credentials.

Observed messages:

```
Permission denied
Permission denied (publickey,password)
```

Screenshot:

```
screenshots/ssh-failed-login.png
```

---

## 3. Ubuntu Authentication Logs

Ubuntu successfully recorded the failed login attempts.

Observed log entries:

```
authentication failure

Failed password for soclab

Connection closed

PAM authentication failures
```

Screenshot:

```
screenshots/auth-log-failed-login.png
```

---

## 4. Wazuh Alert

The Wazuh Threat Hunting dashboard detected the SSH authentication failures.

Observed values:

- Rule ID: **5760**
- Rule Level: **5**
- Description:
  ```
  sshd: authentication failed.
  ```

Screenshot:

```
screenshots/wazuh-ssh-alert.png
```

---

## 5. Investigation Details

The alert investigation provided the following information:

- Username: **soclab**
- Source IP: **192.168.109.128**
- Source Port: **40682**
- Decoder: **sshd**
- Rule Groups:
  ```
  syslog
  sshd
  authentication_failed
  ```

MITRE ATT&CK Mapping:

- T1110.001 – Password Guessing
- T1021.004 – SSH

Screenshot:

```
screenshots/wazuh-ssh-investigation.png
```

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Credential Access | Password Guessing | T1110.001 |
| Lateral Movement | SSH | T1021.004 |

---

# Impact Assessment

No unauthorized access was obtained during this simulation.

The activity consisted only of failed authentication attempts generated for testing the SOC Home Lab detection capabilities.

---

# Containment

Since this was a controlled laboratory simulation, no containment actions were required.

In a production environment, recommended actions include:

- Lock the affected account after repeated failures.
- Enable Multi-Factor Authentication (MFA).
- Restrict SSH access using firewall rules.
- Disable password authentication where possible and use SSH keys.
- Monitor repeated authentication failures for brute-force attacks.

---

# Lessons Learned

- Ubuntu correctly logs SSH authentication failures.
- Wazuh successfully collects logs from `journald`.
- Wazuh Rule **5760** detects failed SSH authentication attempts.
- Threat Hunting enables efficient investigation of authentication events.
- MITRE ATT&CK mapping helps classify adversary behavior.

---

# Conclusion

The SSH authentication failure simulation successfully validated the SOC Home Lab's ability to detect and investigate unauthorized SSH login attempts.

The attack generated authentication failure logs on the Ubuntu server, which were collected by the Wazuh agent and analyzed by the Wazuh Manager. Wazuh generated Rule **5760**, allowing the activity to be investigated through the Threat Hunting dashboard. The investigation confirmed the source IP, targeted user account, MITRE ATT&CK techniques, and event details, demonstrating an effective end-to-end detection and analysis workflow.
