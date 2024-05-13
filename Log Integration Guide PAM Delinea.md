# Log Integration Guide PAM Delinea
## Procedure
### Configure Syslog Connection on Web UI

1. Navigate to **Admin | Configuration** and select the **Foreign Systems** tab.
2. At the SysLog page, click **Create**.

   | Field             | Value           |
   |------------------|--------------------|
   |Protocol |   TCP  |
   |Host   |  SIEM IP  |
   |Port   |  514   |


### Configure Syslog Server Task

After adding a new Syslog connection, to manually send logs to your Syslog Server:

1. Go to **Admin | Tasks**.

2. Expand the **Server Tasks** folder, then **Foreign Systems**, select **SysLog** and click **Create**.

3. From the Template drop-down, for example select **Send SysLog Application Events**.

4. Add a Name for this task, an Event Name (e.g. “Privilege Manager Application Events”), and Event Severity.

5. From the SysLog System drop-down select your SysLog server foreign system (configured above).

6. Click **Create**.
