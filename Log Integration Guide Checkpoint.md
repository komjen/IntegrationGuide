# Log Integration Guide Checkpoint 
## Procedure
### Configure Log Exporter on CLI

1. Login to Checkpoint using CLI/SSH.

2. Go to mode expert.
```shell
expert
```

3. Run this command to configure Checkpoint Firewall sending the logs to SIEM:

```shell
cp_log_export add name defenxor target-server (SIEM IP) target-port 514 protocol tcp format cef

``````

4. Restart Log Exporter
```shell
cp_log_export restart
```