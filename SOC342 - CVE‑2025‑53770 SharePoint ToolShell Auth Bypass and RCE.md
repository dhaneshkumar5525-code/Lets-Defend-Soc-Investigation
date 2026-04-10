# Hi, I'm a Cybersecurity Analyst 
### Focused on analyzing threats, demonstrating attack scenarios, and conducting security investigations.
<img width="1895" height="321" alt="image" src="https://github.com/user-attachments/assets/bb571998-10a5-41fa-b620-cb840d99dbc4" />

### SOC342 - CVE‑2025‑53770 SharePoint ToolShell Auth Bypass and RCE
### Today, we’re going to walk through a real-life incident. First, we’ll understand what happened, and then we’ll begin our investigation by looking at what caused the rule to trigger.
### On July 22, 2025, at 01:07 PM, you’re monitoring your SIEM dashboard when a **critical alert** appears with Event ID 320. The alert is triggered by rule SOC342, linked to CVE-2025-53770 — a SharePoint authentication bypass that could allow remote code execution. Realizing the severity, you quickly take ownership and begin investigating.
### Lets Start:
<img width="805" height="581" alt="image" src="https://github.com/user-attachments/assets/b4f20b2f-be42-4ae2-b10d-8e04b2a131d7" />

### Start by taking ownership of the alert and assigning it to your name. This moves it from the main channel to your investigation queue, so you can track and handle it properly without confusion.
<img width="1736" height="721" alt="image" src="https://github.com/user-attachments/assets/f2e74512-862e-4920-a543-f9c242e3e67e" />

### About Alert:
### CVE‑2025‑53770 SharePoint ToolShell Auth Bypass and RCE
<img width="1900" height="958" alt="image" src="https://github.com/user-attachments/assets/3fe8a032-1a1e-4220-bff6-424eb09b586a" />

### This is a web-based attack targeting Microsoft SharePoint, a server used to store and manage data remotely. The vulnerability, ToolShell (CVE-2025-53770), is a critical(CVSS 9.8) zero-day that allows authentication bypass.
### Named “ToolShell” because it abuses built-in tools to execute commands
### Affects on-premises SharePoint servers
### Caused by insecure deserialization:
### Insecure deserialization means a system blindly trusts and processes data it receives without checking if it’s safe.
### Can lead to remote code execution (RCE)
### Poses a serious risk by allowing unauthorized access
<img width="1764" height="479" alt="image" src="https://github.com/user-attachments/assets/0beaceb1-e776-48da-9c42-bc8a0f4bbe39" />

### Attack Methodology:
<img width="721" height="475" alt="image" src="https://github.com/user-attachments/assets/9c66f6a8-b9c5-409e-9c7b-4d1dfdb565f5" />

### Attack process starts with the share point server with insecure deserilation zero day web vulnerability and crafted script is sent through POST request. The Attacker is crafted script intended to steal Validation Key and Encryption Key inorder to create authentication packets and bypass authentication.
### Once the attacker was is the system, Attacker used spinstall0.aspx payload exexcute this payload using  w3wp.exe process through  powershell.exe cmd.exe.
### This payload provide access through c2 channel for data exfiltartion.

### Before we go into the letsDefend Investigation. I would like to share mitagtion of this attack because its a zero day vunerability and criticality.
<img width="721" height="520" alt="image" src="https://github.com/user-attachments/assets/56a78d1d-6eb2-4e90-83dc-7f33fe2febca" />

### Fix and mitigation steps for the SharePoint ToolShell attack:

### Patch immediately using the latest cumulative updates for your SharePoint version (2016, 2019, or Subscription Edition)
### Rotate MachineKey before and after patching, then restart IIS (iisreset) and check config files for any malicious changes
### Enable AMSI and Microsoft Defender in full mode to detect and block malicious scripts
### Isolate the system by disconnecting it from the internet or placing it behind VPN if protection is limited
### Use EDR/XDR tools to monitor suspicious activity like unusual POST requests to ToolPane.aspx and referer spoofing
### Perform threat hunting for indicators such as webshells (e.g., spinstall0.aspx), unusual logs, and malicious DLL activity
### Follow proper incident response by treating systems as compromised, containing them, and checking for data theft or persistence
### Post-incident hardening by adopting Zero Trust, improving logging, bkups, and overall security posture

### Lets dive into the Lets defend Investigation:
<img width="1764" height="741" alt="image" src="https://github.com/user-attachments/assets/07fb4acc-307f-4bf2-be2f-e0893d6b751f" />
 
### Create case:
<img width="780" height="596" alt="image" src="https://github.com/user-attachments/assets/769234c1-2ebd-4891-ba17-77a3cdfa3b42" />

<img width="972" height="623" alt="image" src="https://github.com/user-attachments/assets/228d0464-c51a-42fc-9d44-46198dfdabbd" />

### Alert Trigger Reason :
### Suspicious unauthenticated POST request targeting ToolPane.aspx with large payload size and spoofed referer indicative of CVE-2025-53770 exploitation.
### The Traffic is incoming from External (Internet) to Internal (Share point server)
### Source IP Address : 107.191.58.76 (External IP)
### Destination IP Address : 172.16.20.17 (Share point server)
### Action: Allowed
<img width="981" height="618" alt="image" src="https://github.com/user-attachments/assets/e8daae22-eec3-4ecd-ad4e-72cea4973108" />

### Checking IP Reputation:
### Source IP 107.191.58.76  Hosted by The Constant Company, LLC, located in Los Angeles, California, United States
<img width="1920" height="897" alt="image" src="https://github.com/user-attachments/assets/834e7fa5-ecc9-48b6-a803-30387ecbd408" />

### 11/94 Vendors in Virus Total are flagged as malicous and here is the reference files that has the Ip address in it.
<img width="1533" height="406" alt="image" src="https://github.com/user-attachments/assets/b0a2e3b4-9990-4016-ac9e-9b33056f646d" />

### Here is the report from Hybrid Analysis and the threat score is 50
<img width="1899" height="876" alt="image" src="https://github.com/user-attachments/assets/2f3405b5-ada0-48af-91da-2b96231f2af8" />

### Here is the Additional Information and open ports of sourceIp
<img width="1900" height="1015" alt="image" src="https://github.com/user-attachments/assets/72db88d4-261b-4164-909f-6c7be07f5fa9" />

### After checking the IP reputation:
### The source IP 107.191.58.76 is 100% Malicous
<img width="979" height="446" alt="image" src="https://github.com/user-attachments/assets/5a9bd508-78bf-47f1-9c04-429957057798" />

### Checking if they are conducting pentesting
<img width="1495" height="385" alt="image" src="https://github.com/user-attachments/assets/cb94b4e7-ca5e-4ed6-b28d-f916ffbfd03a" />

### The Answer is Not planned! There are conducting pentesting on pentest_manchine1 not on Share point01 server.
### It is a real Attack

### Checking traffic direction
<img width="996" height="422" alt="image" src="https://github.com/user-attachments/assets/86935a13-05bc-457f-91a2-ed3b544271f0" />

### Navigate to the Log Activity Tab and look for the communication to Source Ip
<img width="1258" height="845" alt="image" src="https://github.com/user-attachments/assets/1029e347-e00f-48c3-8344-d77778612d65" />

### Traffic is oneway that is Internet to internal (Company Network)
### Examining the Http Traffic
<img width="965" height="636" alt="image" src="https://github.com/user-attachments/assets/98310aa9-291c-4ec1-9d8d-7dea74dfbd90" />

<img width="823" height="188" alt="image" src="https://github.com/user-attachments/assets/36edbd7a-d5a8-4ca3-baa2-65fee325236e" />

### a=/ToolPane.aspx is suspicious and often used in crafted requests to manipulate how the page loads.

### Attack was Successful ?
<img width="961" height="690" alt="image" src="https://github.com/user-attachments/assets/8229d2f2-2ceb-44b0-8048-60bcd1344e9e" />











