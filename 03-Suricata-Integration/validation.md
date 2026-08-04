# Validation

## Objective

Verify that the Suricata and Wazuh integration is working correctly.

## Verification Steps

1. Confirm Suricata service is running.
2. Confirm Wazuh Manager is running.
3. Verify `eve.json` is populated with alert events.
4. Open the Wazuh Dashboard.
5. Search for Suricata alerts.

## Example Alert

```
ET POLICY Possible Kali Linux hostname in DHCP Request Packet
```

## Successful Validation

The following were confirmed:

- Suricata generated alerts.
- Wazuh collected the alerts.
- Alerts appeared in Threat Hunting.
- Rule ID 86601 triggered successfully.

## Conclusion

The Suricata IDS integration with Wazuh was successfully completed and verified.
