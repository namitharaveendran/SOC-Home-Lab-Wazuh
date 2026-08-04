# Wazuh Installation

## Objective

This section documents the installation and configuration of the Wazuh platform.

## Environment

| Component | Details |
|-----------|---------|
| Host OS | Windows 11 |
| Hypervisor | VMware Workstation |
| Wazuh Server | Ubuntu Server |
| Wazuh Version | 4.14.6 |

## Installation Steps

1. Install Ubuntu Server.
2. Update the operating system.
3. Install Wazuh Manager.
4. Install Wazuh Indexer.
5. Install Wazuh Dashboard.
6. Verify all services are running.
7. Access the Wazuh Dashboard.

## Verification

- Wazuh Manager running
- Wazuh Dashboard accessible
- Indexer healthy
- Agent connected

## Lessons Learned

- Importance of network configuration.
- Service verification using systemctl.
- Checking logs during troubleshooting.
