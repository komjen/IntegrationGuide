# Log Integration Guide Aruba ClearPass
## Procedure
### Configure syslog forward on WebUI

#### Configure Syslog Target

1. Navigate to **Administration > External Servers > Syslog Targets**.
   - The Syslog Targets page opens.

2. Click the **Add** link.
   - The Add Syslog Target dialog opens:

   | Field             | Value           |
   |------------------|--------------------|
   |Host Address |   SIEM IP  |
   |Description   |  Integration with Defenxor  |
   |Protocol   |  TCP   |
   |Server Port   |  514   |
   - Click **Save**.

#### Configure Syslog Export Filters

1. Navigate to **Administration > External Servers > Syslog Export Filters**.

2. From the Syslog Export Filters page, click **Add**.
   - The Add Syslog Filters page opens to the General tab:
      
   | Field             | Value           |
   |------------------|--------------------|
   |Name |   Integration with Defenxor  |
   |Description   |  Steram logs to Defenxor  |
   |Export Template   |  Insight Logs   |
   |Syslog Servers   |  Add the one created earlier   |

   - Click **Save**.
