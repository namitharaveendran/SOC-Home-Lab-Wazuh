# Troubleshooting

## Problem

Suricata alerts were not initially visible in the Wazuh Dashboard.

## Investigation

The following checks were performed:

- Verified Suricata service status.
- Verified Wazuh Manager status.
- Confirmed that `eve.json` was being generated.
- Confirmed that Wazuh was monitoring `eve.json`.
- Tested event decoding using `wazuh-logtest`.

## Error

```
ERROR: Too many fields for JSON decoder
```

## Root Cause

Suricata generated verbose JSON events that exceeded the Wazuh JSON decoder limits.

## Resolution

The following actions were taken:

- Reviewed `suricata.yaml`.
- Reduced unnecessary event output.
- Restarted Suricata.
- Restarted Wazuh Manager.
- Verified new alerts.

## Result

Suricata alerts successfully appeared in the Wazuh Dashboard after the configuration changes.
