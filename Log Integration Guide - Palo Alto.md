# Log Integration Guide - Palo Alto
## Procedure
### Create a Log Forwarding Profile

1. Select **Objects > Log Forwarding** and Add a profile.
2. Add one or more match list profiles. The profiles specify log query filters, forwarding destinations, and automatic actions such as tagging.
   - For each match list profile:
     - Enter a Name to identify the profile.
     - Select the Log Type.
     - In the Filter drop-down, select Filter Builder. Specify the following and then Add each query:
       - Connector logic (and/or)
       - Log Attribute
       - Operator to define inclusion or exclusion logic
       - Attribute Value for the query to match
   - Select Syslog.
     - Address: `SIEM IP`
     - Port: `514`
     - Severity: `local7`
     - Format: BSD (Default)
   - Click **OK** to save the Log Forwarding profile.

### Assign the Log Forwarding Profile

1. Select **Policies > Security** and edit the rule.
2. Select **Actions** and select the Log Forwarding profile you created.
3. Set the Profile Type to Profiles or Group, and then select the security profiles or Group.
4. Profile required to trigger log generation and forwarding for:
   - Threat logs.
   - Wildfire Submission logs.
   - For Traffic logs select Log At Session End.
5. Click **OK** to save the rule.

### Configure Destinations for Logs

1. Select **Device > Log Settings**.
2. Configure log forwarding profile that you created before.

### Configure the Firewall to Forward Logs in CEF Format (PAN OS 10)

1. Select **Device > Server Profiles > Syslog**.
2. Select profiles that you created before.
3. Select Custom Log Format.
4. Select log type and copy this template to web interface.

**Traffic**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|1|rt=$cef-formatted-receive_time deviceExternalId=$serial src=$src dst=$dst sourceTranslatedAddress=$natsrc destinationTranslatedAddress=$natdst cs1Label=Rule cs1=$rule suser=$srcuser duser=$dstuser app=$app cs3Label=Virtual System cs3=$vsys cs4Label=Source Zone cs4=$from cs5Label=Destination Zone cs5=$to deviceInboundInterface=$inbound_if deviceOutboundInterface=$outbound_if cs6Label=LogProfile cs6=$logset cn1Label=SessionID cn1=$sessionid cnt=$repeatcnt spt=$sport dpt=$dport sourceTranslatedPort=$natsport destinationTranslatedPort=$natdport flexString1Label=Flags flexString1=$flags proto=$proto act=$action flexNumber1Label=Total bytes flexNumber1=$bytes in=$bytes_sent out=$bytes_received cn2Label=Packets cn2=$packets PanOSPacketsReceived=$pkts_received PanOSPacketsSent=$pkts_sent start=$cef-formatted-time_generated cn3Label=Elapsed time in seconds cn3=$elapsed cs2Label=URL Category cs2=$category externalId=$seqno reason=$session_end_reason PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name cat=$action_source PanOSActionFlags=$actionflags PanOSSrcUUID=$src_uuid PanOSDstUUID=$dst_uuid PanOSTunnelID=$tunnelid PanOSMonitorTag=$monitortag PanOSParentSessionID=$parent_session_id PanOSParentStartTime=$parent_start_time PanOSTunnelType=$tunnel PanOSSCTPAssocID=$assoc_id PanOSSCTPChunks=$chunks PanOSSCTPChunkSent=$chunks_sent PanOSSCTPChunksRcv=$chunks_received PanOSRuleUUID=$rule_uuid PanOSHTTP2Con=$http2_connection PanLinkChange=$link_change_count PanPolicyID=$policy_id PanLinkDetail=$link_switches PanSDWANCluster=$sdwan_cluster PanSDWANDevice=$sdwan_device_type PanSDWANClustype=$sdwan_cluster_type PanSDWANSite=$sdwan_site PanDynamicUsrgrp=$dynusergroup_name
```  
**Threat**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$threatid|$type|$number-of-severity|rt=$cef-formatted-receive_time deviceExternalId=$serial src=$src dst=$dst sourceTranslatedAddress=$natsrc destinationTranslatedAddress=$natdst cs1Label=Rule cs1=$rule suser=$srcuser duser=$dstuser app=$app cs3Label=Virtual System cs3=$vsys cs4Label=Source Zone cs4=$from cs5Label=Destination Zone cs5=$to deviceInboundInterface=$inbound_if deviceOutboundInterface=$outbound_if cs6Label=LogProfile cs6=$logset cn1Label=SessionID cn1=$sessionid cnt=$repeatcnt spt=$sport dpt=$dport sourceTranslatedPort=$natsport destinationTranslatedPort=$natdport flexString1Label=Flags flexString1=$flags proto=$proto act=$action request=$misc cs2Label=URL Category cs2=$category flexString2Label=Direction flexString2=$direction PanOSActionFlags=$actionflags externalId=$seqno cat=$subtype fileId=$pcap_id PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSSrcUUID=$src_uuid PanOSDstUUID=$dst_uuid PanOSTunnelID=$tunnelid PanOSMonitorTag=$monitortag PanOSParentSessionID=$parent_session_id PanOSParentStartTime=$parent_start_time PanOSTunnelType=$tunnel PanOSThreatCategory=$thr_category PanOSContentVer=$contentver PanOSAssocID=$assoc_id PanOSPPID=$ppid PanOSHTTPHeader=$http_headers PanOSURLCatList=$url_category_list PanOSRuleUUID=$rule_uuid PanOSHTTP2Con=$http2_connection PanDynamicUsrgrp=$dynusergroup_name
```
**URL**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|$number-of-severity|rt=$cef-formatted-receive_time deviceExternalId=$serial src=$src dst=$dst sourceTranslatedAddress=$natsrc destinationTranslatedAddress=$natdst cs1Label=Rule cs1=$rule suser=$srcuser duser=$dstuser app=$app cs3Label=Virtual System cs3=$vsys cs4Label=Source Zone cs4=$from cs5Label=Destination Zone cs5=$to deviceInboundInterface=$inbound_if deviceOutboundInterface=$outbound_if cs6Label=LogProfile cs6=$logset cn1Label=SessionID cn1=$sessionid cnt=$repeatcnt spt=$sport dpt=$dport sourceTranslatedPort=$natsport destinationTranslatedPort=$natdport flexString1Label=Flags flexString1=$flags proto=$proto act=$action request=$misc cs2Label=URL Category cs2=$category flexString2Label=Direction flexString2=$direction PanOSActionFlags=$actionflags externalId=$seqno requestContext=$contenttype cat=$threatid fileId=$pcap_id requestMethod=$http_method requestClientApplication=$user_agent PanOSXForwarderfor=$xff PanOSReferer=$referer PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSSrcUUID=$src_uuid PanOSDstUUID=$dst_uuid PanOSTunnelID=$tunnelid PanOSMonitorTag=$monitortag PanOSParentSessionID=$parent_session_id PanOSParentStartTime=$parent_start_time PanOSTunnelType=$tunnel PanOSThreatCategory=$thr_category PanOSContentVer=$contentver PanOSAssocID=$assoc_id PanOSPPID=$ppid PanOSHTTPHeader=$http_headers PanOSRuleUUID=$rule_uuid PanOSURLCatList=$url_category_list PanOSHTTP2Con=$http2_connection PanDynamicUsrgrp=$dynusergroup_name
```
**Wildfire**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|$number-of-severity|rt=$cef-formatted-receive_time deviceExternalId=$serial src=$src dst=$dst sourceTranslatedAddress=$natsrc destinationTranslatedAddress=$natdst cs1Label=Rule cs1=$rule suser=$srcuser duser=$dstuser app=$app cs3Label=Virtual System cs3=$vsys cs4Label=Source Zone cs4=$from cs5Label=Destination Zone cs5=$to deviceInboundInterface=$inbound_if deviceOutboundInterface=$outbound_if cs6Label=LogProfile cs6=$logset cn1Label=SessionID cn1=$sessionid cnt=$repeatcnt spt=$sport dpt=$dport sourceTranslatedPort=$natsport destinationTranslatedPort=$natdport flexString1Label=Flags flexString1=$flags proto=$proto act=$action request=$misc cs2Label=URL Category cs2=$category flexString2Label=Direction flexString2=$direction PanOSActionFlags=$actionflags externalId=$seqno cat=$threatid filePath=$cloud fileId=$pcap_id fileHash=$filedigest fileType=$filetype suid=$sender msg=$subject duid=$recipient oldFileId=$reportid PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSSrcUUID=$src_uuid PanOSDstUUID=$dst_uuid PanOSTunnelID=$tunnelid PanOSMonitorTag=$monitortag PanOSParentSessionID=$parent_session_id PanOSParentStartTime=$parent_start_time PanOSTunnelType=$tunnel PanOSThreatCategory=$thr_category PanOSContentVer=$contentver PanOSAssocID=$assoc_id PanOSPPID=$ppid PanOSHTTPHeader=$http_headers PanOSRuleUUID=$rule_uuid
```
**Config**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$result|$type|1|rt=$cef-formatted-receive_time deviceExternalId=$serial shost=$host cs3Label=Virtual System cs3=$vsys act=$cmd duser=$admin destinationServiceName=$client msg=$path externalId=$seqno PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSActionFlags=$actionflags cs1Label=Before Change Detail cs1=$before-change-detail cs2Label=After Change Detail cs2=$after-change-detail
```
**HIP Match**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$matchtype|$type|1|rt=$cef-formatted-receive_time deviceExternalId=$serial suser=$srcuser cs3Label=Virtual System cs3=$vsys shost=$machinename src=$src cnt=$repeatcnt externalId=$seqno cat=$matchname start=$cef-formatted-time_generated cs2Label=Operating System cs2=$os PanOSActionFlags=$actionflags PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name cn2Label=Virtual System ID cn2=$vsys_id c6a2Label=IPv6 Source Address c6a2=$srcipv6 PanOSHostID=$hostid
```
**Tunnel**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|1|rt=$cef-formatted-receive_time deviceExternalId=$serial src=$src dst=$dst sourceTranslatedAddress=$natsrc destinationTranslatedAddress=$natdst cs1Label=Rule cs1=$rule suser=$srcuser duser=$dstuser app=$app cs3Label=Virtual System cs3=$vsys cs4Label=Source Zone cs4=$from cs5Label=Destination Zone cs5=$to deviceInboundInterface=$inbound_if deviceOutboundInterface=$outbound_if cs6Label=Log Action cs6=$logset cn1Label=SessionID cn1=$sessionid cnt=$repeatcnt spt=$sport dpt=$dport sourceTranslatedPort=$natsport destinationTranslatedPort=$natdport flexString1Label=Flags flexString1=$flags proto=$proto act=$action externalId=$seqno PanOSActionFlags=$actionflags PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSTunnelID=$tunnelid PanOSMonitorTag=$monitortag PanOSParentSessionID=$parent_session_id PanOSParentStartTime=$parent_start_time cs2Label=Tunnel Type cs2=$tunnel flexNumber1Label=Total bytes flexNumber1=$bytes in=$bytes_sent out=$bytes_received cn2Label=Packets cn2=$packets PanOSPacketsSent=$pkts_sent PanOSPacketsReceived=$pkts_received flexNumber2Label=Maximum Encapsulation flexNumber2=$max_encap cfp1Label=Unknown Protocol cfp1=$unknown_proto cfp2Label=Strict Checking cfp2=$strict_check PanOSTunnelFragment=$tunnel_fragment cfp3Label=Sessions Created cfp3=$sessions_created cfp4Label=Sessions Closed cfp4=$sessions_closed reason=$session_end_reason cat=$action_source start=$cef-formatted-time_generated cn3Label=Elapsed time in seconds cn3=$elapsed PanOSTunneInspectionRule=$tunnel_insp_rule PanOSRmtUserIP=$remote_user_ip PanOSRmtUserID=$remote_user_id PanOSRuleUUID=$rule_uuid PanOSPcapID=$pcap_id PanDynamicUsrgrp=$dynusergroup_name
```
**User ID**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|1|rt=$cef-formatted-receive_time deviceExternalId=$serial cs1Label=Factor Type cs1=$factortype cs3Label=Virtual System cs3=$vsys cs4Label=Data Source Name cs4=$datasourcename cs5Label=Data Source cs5=$datasource cs6Label=Data Source Type cs6=$datasourcetype cn1Label=Factor Number cn1=$factorno cn2Label=Virtual System ID cn2=$vsys_id cn3Label=Timeout Threshold cn3=$timeout src=$ip spt=$beginport dpt=$endport cnt=$repeatcnt duser=$user externalId=$seqno cat=$eventid end=$factorcompletiontime PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSActionFlags=$actionflags PanOSUGFlags=$ugflags PanOSUserBySource=$userbysource
```
**GlobalProtect**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$type|$subtype|rt=$receive_time PanOSDeviceSN=$serial PanOSLogTimeStamp=$time_generated PanOSVirtualSystem=$vsys PanOSEventID=$eventid PanOSStage=$stage PanOSAuthMethod=$auth_method PanOSTunnelType=$tunnel_type PanOSSourceUserName=$srcuser PanOSSourceRegion=$srcregion PanOSEndpointDeviceName=$machinename PanOSPublicIPv4=$public_ip PanOSPublicIPv6=$public_ipv6 PanOSPrivateIPv4=$private_ip PanOSPrivateIPv6=$private_ipv6 PanOSHostID=$hostid PanOSDeviceSN=$serialnumber PanOSGlobalProtectClientVersion=$client_ver PanOSEndpointOSType=$client_os PanOSEndpointOSVersion=$client_os_ver PanOSCountOfRepeats=$repeatcnt PanOSQuarantineReason=$reason PanOSConnectionError=$error PanOSDescription=$opaque PanOSEventStatus=$status PanOSGPGatewayLocation=$location PanOSLoginDuration=$login_duration PanOSConnectionMethod=$connect_method PanOSConnectionErrorID=$error_code PanOSPortal=$portal PanOSSequenceNo=$seqno PanOSActionFlags=$actionflags
```
**System**
```shell
CEF:0|Palo Alto Networks|PAN-OS|$sender_sw_version|$subtype|$type|$number-of-severity|rt=$cef-formatted-receive_time deviceExternalId=$serial cs3Label=Virtual System cs3=$vsys fname=$object flexString2Label=Module flexString2=$module msg=$opaque externalId=$seqno cat=$eventid PanOSDGl1=$dg_hier_level_1 PanOSDGl2=$dg_hier_level_2 PanOSDGl3=$dg_hier_level_3 PanOSDGl4=$dg_hier_level_4 PanOSVsysName=$vsys_name dvchost=$device_name PanOSActionFlags=$actionflags
```