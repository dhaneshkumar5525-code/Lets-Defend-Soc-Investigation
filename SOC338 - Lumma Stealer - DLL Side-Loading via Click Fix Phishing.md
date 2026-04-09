# Hi, I'm a Cybersecurity Analyst 
### Focused on analyzing threats, demonstrating attack scenarios, and conducting security investigations.
### SOC338 - Lumma Stealer - DLL Side-Loading via Click Fix Phishing
### About the Alert:
<img width="1524" height="67" alt="image" src="https://github.com/user-attachments/assets/45169006-18c3-4320-803f-72700937ab08" />

### Lumma Stealer: A type of malware that steals sensitive information from Windows systems
### DLL Side-Loading: A technique where a malicious DLL file is loaded by a trusted application instead of a legitimate one
### Click Fix Phishing: A phishing trick that urges users to “click to fix” an issue (e.g., fake update alert) to make them run malicious content
### Alert Overview:
<img width="1521" height="491" alt="image" src="https://github.com/user-attachments/assets/63e1f7f5-3071-450b-b12d-d84d5219d40d" />

### Alert Severity : Critical
### EventID: 316 EventTime: Mar, 13, 2025, 09:44 AM
### By observing Alert details
### Initial Hypothesis:
### The user Dylan received a phishing email containing a “click to fix” link. This link redirected to a malicious website that delivered a Click Fix script, which was used to distribute the Lumma Stealer malware.
### Lets start the Investigation by assigning the ownership
<img width="1553" height="100" alt="image" src="https://github.com/user-attachments/assets/4aa5417a-444a-461f-bc33-5f43f67bd95f" />

<img width="784" height="589" alt="image" src="https://github.com/user-attachments/assets/3a8e4e9f-a1f3-47ff-ae8b-6f74f3bc82f1" />

### Now We are in the Investigation Tab and Create case:
<img width="1564" height="265" alt="image" src="https://github.com/user-attachments/assets/ab319fad-3cd6-4fda-97e8-70fe42ec4206" />

<img width="866" height="652" alt="image" src="https://github.com/user-attachments/assets/84451650-7f02-4f5a-b8e3-e5c8bda6ebae" />

### Lets Start the Playbook:
<img width="1500" height="458" alt="image" src="https://github.com/user-attachments/assets/ecf4a1be-ce64-4967-a5aa-5930c3dc56a1" />

### Tip: I duplicated the tab so I could keep the playbook visible while working on the alert simultaneously. 
### Question 1: When was it sent?
### By checking the alert details from the Investigation Channel, I was able to determine the exact timestamp.
### Mar, 13, 2025, 09:44 AM
<img width="1435" height="158" alt="image" src="https://github.com/user-attachments/assets/5c1c96c0-a79d-4477-8a87-cc1890687807" />

### Question 2: What is the email’s SMTP address?
### Found in the same alert detail pane.
### 132.232.40.201
### <img width="1462" height="68" alt="image" src="https://github.com/user-attachments/assets/f6f37dd9-07f3-420c-99ab-31952e12a174" />

### Question 3: What is the sender address?
### update@windows-update.site
<img width="1288" height="67" alt="image" src="https://github.com/user-attachments/assets/9b7672de-4409-4b3f-8548-b19642d140a3" />

### Question 4: What is the recipient address?
### dylan@letsdefend.io
<img width="1504" height="71" alt="image" src="https://github.com/user-attachments/assets/1ef6dcc2-7c86-47f9-9356-5c48337ee891" />

### Question 5: Is the mail content suspicious?
### Naviagte to the Email Security Tab and enter the username and select the mail
<img width="1891" height="731" alt="image" src="https://github.com/user-attachments/assets/a937567b-a3db-4b6e-9c5f-ac592aef0a82" />

### Yes, definitely. By opening the email from the Email Security section, I identified multiple red flags:
<img width="1436" height="185" alt="image" src="https://github.com/user-attachments/assets/734e0e3c-91ac-4754-a6e1-60476f08fde7" />

### Urgent language pushing for immediate action
### Excessive repetition of the “Update Now” button
<img width="1441" height="515" alt="image" src="https://github.com/user-attachments/assets/553e094b-38d4-4780-b00a-353f9c12b602" />


### Sender’s domain not belonging to Microsoft
<img width="1428" height="542" alt="image" src="https://github.com/user-attachments/assets/e6118141-9290-4f05-8ec2-9e3a7ca8f84a" />

### All these elements indicate a phishing attempt.

### Question 6: Are there any attachments?
### Yes, there is a hyperlink under the “UPDATE NOW” button.
### Hovering on the Update Button, The link was shown in below.
<img width="1414" height="50" alt="image" src="https://github.com/user-attachments/assets/cda6e9ed-0fb9-4a93-80ae-699ad26e82f1" />

### Step 2:
<img width="791" height="374" alt="image" src="https://github.com/user-attachments/assets/50fb7eee-de2d-4a60-918a-c50256aa3ba1" />

### I answered “yes” based on the clear indicators identified in the previous step.

### Step 3:
<img width="848" height="456" alt="image" src="https://github.com/user-attachments/assets/cf8acd56-d681-44f8-9922-0257ff03c347" />

### I first submitted the suspicious URL to VirusTotal,
<img width="1200" height="777" alt="image" src="https://github.com/user-attachments/assets/b3376f49-ef58-40ca-b323-e1e488c562d8" />

### which returned 10/97 detections flagging it as malicious (phishing).
<img width="1100" height="518" alt="image" src="https://github.com/user-attachments/assets/2839f3c9-0b9d-4657-871e-84ee64e802cf" />

### To get deeper behavioral insight, I also submitted the link to Hybrid Analysis, which returned a threat score of 100/100 and confirmed it as malicious.

<img width="1012" height="81" alt="image" src="https://github.com/user-attachments/assets/b3525776-b94f-434e-b7be-bfb15c195f94" />

### Step 4:
<img width="792" height="253" alt="image" src="https://github.com/user-attachments/assets/754c41b8-5682-4765-940e-67a846b9b3fb" />

### In the alert details, under the Action field, I found the value set to Allowed — confirming that the email was successfully delivered to the recipient.
<img width="1435" height="167" alt="image" src="https://github.com/user-attachments/assets/c1b36ceb-9506-46d7-874b-60b4f2fa0093" />

### Step 5:
<img width="762" height="238" alt="image" src="https://github.com/user-attachments/assets/a2ce1d4b-ccbc-45a6-9063-4c903531c6a8" />
### Navigate to the Email Security, Select the user email and Click Delete button to remove the mail from the user mail box.
<img width="1515" height="619" alt="image" src="https://github.com/user-attachments/assets/09979dc5-d183-40ab-b1cd-0fe8fa156815" />

<img width="1522" height="174" alt="image" src="https://github.com/user-attachments/assets/cc13ae18-b92a-4959-8b56-1d40468bd5fe" />

### Given the malicious content, I deleted the email from the user’s inbox to prevent interaction.

### Step 6:
### Given the malicious content, I deleted the email from the user’s inbox to prevent interaction.
<img width="752" height="392" alt="image" src="https://github.com/user-attachments/assets/9b6ae31b-5a51-4dac-8071-adcf71e2ce84" />

### Next, I moved to the Endpoint Security section and searched for Dylan’s workstation.
### Navigate to the Endpoint and Enter the username.
<img width="1305" height="638" alt="image" src="https://github.com/user-attachments/assets/2d0c07ac-58e0-4176-bf47-7d32b4bc626a" />

### In the Browser History, I confirmed that the malicious URL had been accessed.
<img width="1073" height="241" alt="image" src="https://github.com/user-attachments/assets/c5b64860-d0f5-45bb-95c3-1609606a6738" />

### Step 7:
<img width="795" height="287" alt="image" src="https://github.com/user-attachments/assets/12618482-69ff-419f-8f82-848efb78ea2d" />

### To contain Dylan’s endpoint, I simply toggled the “Contain” button in the Endpoint Security tab.
<img width="1142" height="620" alt="image" src="https://github.com/user-attachments/assets/3dc56f0a-e2c3-41a2-b068-ee5781351176" />

### Further Investigation:
### Who else received the mail in the organistaion from the Attacker
<img width="1472" height="796" alt="image" src="https://github.com/user-attachments/assets/d7754ed6-ffab-4e26-9293-788bfdcff2c3" />

### Only dylan@letsdefend.io was sent the mail from the Attacker 132.232.40.201

### Final step:
### I completed the playbook, documented my observations, and closed the alert, marking it as a True Positive.
### Once closed, I confirmed the success of my investigation in the Closed Alerts section.
## Congratulations !!! We have Completed the Room.
<img width="1739" height="578" alt="image" src="https://github.com/user-attachments/assets/f23bc8a8-9e5b-46bc-964f-400aa474b23a" />

What is the recipient address? 
dylan@letsdefend.io
Is the mail content suspicious?
Yes
Are there any attachment?No
