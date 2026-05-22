# auditd Rules
/etc/audit/audit.rules
```xml
-D
-b 8192
-f 1
-w /bin/bash -p x -k shell_exec
-w /usr/bin/nc -p x -k netcat_exec
-w /usr/bin/curl -p x -k curl_exec
-w /usr/bin/wget -p x -k wget_exec
--backlog_wait_time 60000

```
---
