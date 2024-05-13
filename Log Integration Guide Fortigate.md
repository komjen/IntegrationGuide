# Log Integration Guide Fortigate
## Procedure
### Configure syslog forward on Web UI

1. Go to System Settings > Log Forwarding.

2. Click Create New in the toolbar. The Create New Log Forwarding pane opens. 

3. Fill in the information as per the below table, then click OK to create the new log forwarding. 

| Field             | Value           |
|------------------|--------------------|
| Name             | Defenxor
| Status           | On                 |
| Remote Server Type | CEF            |
| Server IP        | SIEM IP |
| Port             | 514                |
| Reliable Connection   |   On  |

4. Setup Fortigate to send the logs using CEF format, login to CLI FortiOS and running this command:

```shell
config log syslogd2 setting
set format cef
end
```