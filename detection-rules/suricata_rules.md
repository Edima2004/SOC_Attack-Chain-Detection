SYN Scan Detection
```xml
alert tcp any any -> $HOME_NET any ( msg:"CUSTOM SYN Scan Detected"; flags:S; threshold:type both, track by_src, count 10, seconds 2; sid:1000201; rev:1;)
```
<br><br>

Xmas Scan Detection
```xml
alert tcp any any -> $HOME_NET any ( msg:"XMAS Scan Detected"; flags:FPU; flow:stateless; threshold:type both, track by_src, count 10, seconds 2; sid:1000201; rev:1;) \
```
<br><br>

FIN Scan Detection
```xml
alert tcp any any -> $HOME_NET any ( msg:"FIN Scan Detected"; flags:F; flow:stateless; threshold:type both, track by_src, count 10, seconds 2; sid:1000201; rev:1;)
```
<br><br>

NULL Scan Detection
```xml
alert tcp any any -> $HOME_NET any ( msg:"NULL Scan Detected"; flags:0; flow:stateless; threshold:type both, track by_src, count 10, seconds 2; sid:1000201; rev:1;)
```
---
_The above rules should be placed in /etc/suricata/rules/local.rules_
