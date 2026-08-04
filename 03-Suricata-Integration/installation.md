# Suricata Installation

## Objective

Install the Suricata Intrusion Detection System (IDS) on the Ubuntu Server and verify that it is running correctly before integrating it with Wazuh.

## Lab Environment

| Component | Details |
|----------|---------|
| Operating System | Ubuntu Server 22.04 |
| IDS | Suricata |
| SIEM | Wazuh 4.14.6 |
| Hypervisor | VMware Workstation |
| Attack Machine | Kali Linux |

## Installation Steps

### 1. Update the system

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Install Suricata

```bash
sudo apt install suricata -y
```

### 3. Verify the installation

```bash
suricata --build-info
```

### 4. Check the service status

```bash
sudo systemctl status suricata
```

Expected result:

- Service is **active (running)**.

## Verification

The following checks were performed:

- Suricata installed successfully.
- Service status verified using `systemctl`.
- Configuration file located at:

```
/etc/suricata/suricata.yaml
```

- Event logs generated under:

```
/var/log/suricata/
```

## Outcome

Suricata was successfully installed and verified. The IDS was ready for integration with the Wazuh SIEM platform.
