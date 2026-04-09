# Hi, I'm a Cybersecurity Analyst 
### Focused on analyzing threats, demonstrating attack scenarios, and conducting security investigations.
<img width="725" height="500" alt="image" src="https://github.com/user-attachments/assets/680e236d-9fdf-42d7-9ac5-ac0f42d72219" />

### SOC138 — Detected Suspicious Xls File: LetsDefend
<img width="980" height="980" alt="image" src="https://github.com/user-attachments/assets/c44d906c-dd56-4b6e-a3b8-93867c746c9e" />

### What is an XLS File :
### - XLS is a Microsoft Excel spreadsheet file.
### - Used to store data in rows and columns.
### - Can contain text, numbers, formulas, and charts.
### - Looks harmless but can be used for attacks.

### We will investigate this incident promptly.
### An alert has been triggered: on March 13, 2021 at 8:20 PM, our systems detected a suspicious XLS file.
###  Investigation is in progress
###  Suspicious file detected by system alert
###  Time of detection: March 13, 2021, 8:20 PM
### I previously investigated this incident and am now re-investigating it to demonstrate the process and ensure proper documentation.
<img width="926" height="399" alt="image" src="https://github.com/user-attachments/assets/6ee0aad9-539f-4758-934d-479dcfb07e13" />

### Workflow steps:
<img width="1599" height="293" alt="image" src="https://github.com/user-attachments/assets/80201c30-492e-4e10-a56d-70bd34dc921c" />

### Alert appears in Main Channel
### Assign it to yourself
### Alert moves to Investigation Channel for review
### After completing the investigation, the alert is moved to Closed Alerts

### Let’s dive into the alert, start gathering information, and figure out whether this file is really malicious!
<img width="1727" height="931" alt="image" src="https://github.com/user-attachments/assets/1797247b-e32e-49d2-9680-40fbce549e9d" />

### First, we have a file hash. We can check it on sites like VirusTotal, Any.Run, or HybridAnalysis to understand the file better. We'll start with VirusTotal.
### Right away, we see that 47 out of 66 security vendors flagged this file as malicious—a strong indication, but we shouldn’t rely on a single data point.

<img width="1332" height="812" alt="image" src="https://github.com/user-attachments/assets/619545e8-bfc3-4941-a368-00d6140b7095" />

### In the Relations tab, we see “Contacted URLs” and “Contacted Domains.” Assuming this file could be malware, these may indicate potential Command and Control (C2) activity. With that in mind
<img width="1335" height="535" alt="image" src="https://github.com/user-attachments/assets/0aa0e94d-7fda-40d9-9355-4b14e16d7c04" />

### we’ll check the Behavior tab to see if our suspicions are confirmed.
### We again see a clear “malicious” indicator, with two reports closely matching the date of our incident. This is a strong sign, so we can move on to other points of interest while keeping these tabs open to track any new or matching information.

<img width="1892" height="831" alt="image" src="https://github.com/user-attachments/assets/4f2e4047-44e2-4e92-8d14-e5cfbde73d26" />

### Gathering Information (Logs)
### Next, we’ll check our internal resources. To see what the endpoint was doing, we’ll go to the **log management** section. We have an IP address to search, so let’s look it up and see what activity comes up.
<img width="1597" height="770" alt="image" src="https://github.com/user-attachments/assets/5d08bec2-6e54-4328-acfa-2f6658142e26" />

### We already found two logs matching the date and time from earlier, containing some interesting data. Most importantly, we have a new entry for our notepad: the **Destination_address** in both logs is “177.53.143.89.” Let’s check if this IP also appears in our VirusTotal report.
<img width="1318" height="520" alt="image" src="https://github.com/user-attachments/assets/16449969-2f34-484e-9e10-4513bd19c451" />

<img width="468" height="24" alt="image" src="https://github.com/user-attachments/assets/7e59eed9-dbcc-4303-b6e6-a49a849af405" />

### Back in VirusTotal’s **Relations** tab, under “Contacted IP addresses,” we see the same IP from our logs listed as the third entry. Notably, it’s located in   
### **Brazil (BR)**, matching the URL “multiwaretecnologia.com.br” we noted earlier. This strongly suggests potential C2 activity. We can now create our case for this alert and make our final decision.
<img width="1570" height="356" alt="image" src="https://github.com/user-attachments/assets/c416ed8e-d066-4a08-af1a-a7710cbd00fa" />

### Starting our playbook we are greeted with a dropdown menu that asks us to “Define Threat Indicator”
<img width="802" height="350" alt="image" src="https://github.com/user-attachments/assets/edfdec27-569d-44fb-8b18-0d5a3b3ac611" />

### Options 2 and 3 don’t reflect the suspicious file we detected.
### The evidence supports unexpected outgoing traffic, showing connections to the IP and domain tied to potential C2.
### After moving on to the next section we see “Check if the malware is quarantined/cleaned”
<img width="810" height="427" alt="image" src="https://github.com/user-attachments/assets/e9408751-26f3-42ef-a9a6-e4908837eb2a" />

### How do we do know? Let’s go back and look at the expanded alert
<img width="593" height="19" alt="image" src="https://github.com/user-attachments/assets/e5fc9895-7ed0-49e0-87f5-2f1a5f498df4" />

### “Device action: allowed” means the system detected the file but didn’t block or quarantine it. We already knew this from the logs showing Sofia’s endpoint communicating with the IP linked to the .br URL, but it’s good practice to confirm. 
### We’ll select “Not Quarantined”
### The next window says “Analyze Malware”
<img width="806" height="481" alt="image" src="https://github.com/user-attachments/assets/3947d686-a9d2-428e-b0c0-8f73f48dc9bc" />

### Since we’ve already done OSINT gathering with VirusTotal and HybridAnalysis, we’ll mark the file as **Malicious** and proceed to the next step. It’s also worth noting the other listed sites, as they’re valuable resources to add to our toolkit.
### Our next step is to “Check if Someone Requested the C2”
<img width="804" height="496" alt="image" src="https://github.com/user-attachments/assets/ec9be019-ff99-4ed8-a73b-1a61ea00ed09" />

### This step may seem wordy, but it’s simply asking whether our endpoint communicated with a malicious server. We confirmed that it did, connecting to a C2 address that matches the domain we found. We’ll select **“Accessed”** and move on to the next step, **Containment**.
<img width="802" height="437" alt="image" src="https://github.com/user-attachments/assets/7a43517b-4d81-4070-ad0c-0e1b4feaa3d7" />

### Now that we’ve confirmed malicious activity, we need to contain the affected system. Let’s go to **Endpoint Security** to perform the containment.
<img width="1611" height="789" alt="image" src="https://github.com/user-attachments/assets/eb656852-c0c1-4d86-bb47-059dd08bb421" />

### In **Endpoint Security**, after finding Sofia’s device (by her name or the internal IP noted earlier), go to the **Action** section in the top right and click the slider next to **Containment**.
<img width="1617" height="795" alt="image" src="https://github.com/user-attachments/assets/bff0df39-0a64-4498-a831-cc0327f7889d" />

### With the file contained, we can return to our playbook, click **Next**, and complete the case by adding our artifacts and notes.
<img width="807" height="582" alt="image" src="https://github.com/user-attachments/assets/1bd9b7e8-4f4f-45d9-9a7a-d96e171325d3" />

### Here, we can add artifacts we found or consider relevant. For example, if the file reappears under a different name but still communicates with the same IP/URL, rules can be created to catch it early. These artifacts also serve as valuable reference points for escalation. Next, we’ll move on to **Analysis Notes**.
<img width="807" height="504" alt="image" src="https://github.com/user-attachments/assets/f2b46b33-a68a-4c65-82e3-2b6d63ec3985" />

### This section is for providing detailed, concise, and informative notes about the incident, including what happened, what actions were taken, and recommended next steps. Here are your key notes summarized for the playbook:

### Date/Time: Mar 13, 2021, 08:20 PM
### Malicious File Hash: 7ccf88c0bbe3b29bf19d877c4596a8d4
### Malicious URL: multiwaretecnologia.com.br
### C2 IP Address: 177.53.143.89
### Endpoint: 172.16.17.56

### Summary:
### Suspicious XLS file confirmed malicious by VirusTotal and HybridAnalysis. Execution caused HTTP requests to C2 IP, compromising the endpoint.

### Immediate Actions Taken:

### Isolated the affected machine to prevent spread

### Suggestions / Next Steps:

### Conduct further analysis to check for potential data exfiltration
### Change passwords for users on affected endpoints
### Ensure file eradication and restore affected machine from backup prior to incident

### We can now finish the playbook and close the alert.
<img width="605" height="438" alt="image" src="https://github.com/user-attachments/assets/f1c21a2a-e2bd-4702-88b6-518fe58d1d83" />

### Conclusion:
### Artifact Collection
### All identified indicators were added as artifacts, including:
### File hash
### Suspicious IP address
### Related URLs
<img width="1186" height="490" alt="image" src="https://github.com/user-attachments/assets/714950e7-c77c-4b6a-aba7-b7bd2f43a205" />


### In this alert, what appeared to be a harmless spreadsheet turned out to be malicious, running scripts that communicated with a C2 server. Using telemetry and research tools, we were able to identify the threat and respond effectively.
## Congratulations !!! We Have Completed the Room.

<img width="1408" height="531" alt="image" src="https://github.com/user-attachments/assets/29107d75-9402-45fb-a76d-f487b42625e2" />













