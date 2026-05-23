
# Wazuh Server Configuration
_configuration should be placed in /var/ossec/etc/ossec.conf_
```xml
  <localfile>
    <log_format>apache</log_format>
    <location>/var/log/apache2/error.log</location>
  </localfile>

  <localfile>
    <log_format>apache</log_format>
    <location>/var/log/apache2/access.log</location>
  </localfile>

  <localfile>
    <log_format>syslog</log_format>
    <location>/var/ossec/logs/active-responses.log</location>
  </localfile>

  <localfile>
    <log_format>syslog</log_format>
    <location>/var/log/dpkg.log</location>
  </localfile>

```
---

# Wazuh Agent Configuration
_configuration should be placed in /var/ossec/etc/ossec.conf_
```xml
  <localfile>
    <log_format>apache</log_format>
    <location>/var/log/apache2/access.log</location>
  </localfile>

  <localfile>
    <log_format>apache</log_format>
    <location>/var/log/apache2/error.log</location>
  </localfile>

  <localfile>
    <log_format>audit</log_format>
    <location>/var/log/audit/audit.log</location>
  </localfile>

  <localfile>
    <log_format>full_command</log_format>
    <command>ps -ef | grep scp</command>
    <frequency>30</frequency>
  </localfile>

  <localfile>
    <log_format>json</log_format>
    <location>/var/log/osquery/osqueryd.results.log</location>
  </localfile>
```

---

# osquery Configuration
_configuration should be placed in /etc/osquery/osquery.conf_
```json
{
  "options": {
    "logger_plugin": "filesystem",
    "logger_path": "/var/log/osquery",
    "enable_monitor": "true"
  },

  "schedule": {
    "scp_process_detection": {
      "query": "SELECT pid, name, path, cmdline FROM processes WHERE name='scp';",
      "interval": 20
    },

    "ssh_connections": {
      "query": "SELECT pid, remote_address, remote_port FROM process_open_sockets WHERE remote_port=22;",
      "interval": 20
    }

  }
}
```
---

# local decoder config
_configuration should be placed in /var/ossec/etc/decoders/local_decoder.xml_
```xml
<decoder name="scp-exfiltration">
    <prematch>^scp </prematch>
    <regex>scp\s+-r\s+(\w+)@([0-9.]+):~/(.+)\s+\.</regex>
    <order>user,srcip,file</order>
</decoder>

<decoder name="reverse-shell-bash">
    <prematch>bash -i</prematch>
    <regex>bash\s+-i\s+>&\s+/dev/tcp/([0-9.]+)/([0-9]+)</regex>
    <order>dest_ip,dest_port</order>
</decoder>

```
