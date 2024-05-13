# Log Integration Guide Cisco Ironport 
## Procedure
### Condfigure syslog forward on Web UI


1. Select **System Administration > Log Subscription**.

2. Click **Add Log Subscription**.

3. Choose the log type:
   - **mail_logs, antispam, antivirus, authentication**

4. Type the Log Name in the Log Name field.

5. Use the default configuration for:
   - File Name
   - Maximum File Size
   - Log Level

6. Choose **syslog push** in the **Retrieval Mode field**.

7. Input the IP Address of **SIEM IP** in the Hostname field.
8. Choose **TCP** in the Protocol field.
9. Use the **debug** for **Facility**.
10. Click **OK**.
