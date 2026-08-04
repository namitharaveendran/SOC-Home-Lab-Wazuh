# Suricata Configuration

## Objective

Configure Suricata to generate EVE JSON logs and integrate them with Wazuh for security monitoring.

## Configuration File

```
/etc/suricata/suricata.yaml
```

## Main Configuration

### EVE JSON Output

Suricata was configured to generate JSON events using the EVE logging format.

```yaml
eve-log:
  enabled: yes
  filename: eve.json
```

### Log Location

```
/var/log/suricata/eve.json
```

### Enabled Event Types

The following event types were enabled:

- alert
- flow
- dns
- http
- tls
- dhcp
- anomaly

## Wazuh Configuration

The Wazuh Manager was configured to monitor:

```
/var/log/suricata/eve.json
```

using:

```xml
<localfile>
  <location>/var/log/suricata/eve.json</location>
  <log_format>json</log_format>
</localfile>
```

## Verification

Configuration was verified using:

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

## Outcome

Suricata successfully generated JSON logs that could be collected by Wazuh.
