SQL Injection Detection 
```xml
<group name="web,sql_injection,attack">
  <rule id="100300" level="12">
    <if_sid>31100</if_sid>
    <match>UNION SELECT|OR 1=1|information_schema</match>
    <description>Possible SQL Injection Attempt Detected</description>
  </rule>
</group>

```
---
Successful SSH Brute Force & Login Detection 
```xml
<group name="local,syslog,sshd,">
  <rule id="100001" level="5">
    <if_sid>5716</if_sid>
    <srcip>1.1.1.1</srcip>
    <description>sshd: authentication failed from IP 1.1.1.1.</description>
    <group>authentication_failed,pci_dss_10.2.4,pci_dss_10.2.5,</group>
  </rule>
</group>

```
---
SCP Exfiltration Detection
```xml
<group name="scp,exfiltration">
  <rule id="100600" level="10">
    <match>scp</match>
    <description>Possible SCP data exfiltration detected</description>
    <mitre>
      <id>T1048</id>
    </mitre>
    <group>exfiltration,ssh_transfer</group>
  </rule>
</group>

<group name="osquery,exfiltration">
  <rule id="100700" level="10">
    <field name="name">scp</field>
    <description>Possible SCP process detected via osquery</description>
    <mitre>
      <id>T1048</id>
    </mitre>
    <group>exfiltration,scp_activity</group>
  </rule>
  <rule id="100701" level="8">
    <field name="remote_port">22</field>
    <description>SSH network connection detected via osquery</description>
    <mitre>
      <id>T1078</id>
    </mitre>
    <group>ssh_activity,network_connection</group>
  </rule>
</group>

```
---
Active Scanning Detection
```xml
<group name="recon,network_scan">
  <rule id="100500" level="10">
    <if_group>suricata</if_group>
    <match>Scan Detected</match>
    <description>Network reconnaissance activity detected (Suricata)</description>
  </rule>
</group>
```
