# Hi, I'm a Cybersecurity Analyst 
### Focused on analyzing threats, demonstrating attack scenarios, and conducting security investigations.
### Today We are going to Investigated SOC282 - Phishing Alert - Deceptive Mail Detected Alert
<img width="1503" height="70" alt="image" src="https://github.com/user-attachments/assets/e0265d17-52dc-405a-ab5d-6f9404a7cd68" />

### The alert is first received in the main channel. It is then promptly acknowledged, and ownership is assigned to oneself. Following this, the process moves to the Investigation tab for further analysis.
<img width="778" height="568" alt="image" src="https://github.com/user-attachments/assets/3eb74e5c-485c-4988-bedd-d2439b459141" />

### Creste Case for the Alert and navigate to the case management tab
<img width="781" height="568" alt="image" src="https://github.com/user-attachments/assets/b39a9648-240e-4361-af5b-0e72d78f4e01" />

### About the Alert
### Phishing: A cyberattack where attackers impersonate a trusted source to trick individuals into revealing sensitive information such as passwords or financial details.
### Deceptive Mail: An email designed to mislead the recipient by appearing legitimate, often used to manipulate actions like clicking malicious links or sharing confidential data.
<img width="1498" height="636" alt="image" src="https://github.com/user-attachments/assets/77ae37fb-2bfc-4266-9417-f9fb57225d0f" />

### Intial analysis : 
### Phishing alert-severity medium
### Internal user felix received received and the action is allowed.
### What is the sender address?-
### free@coffeeshooop.com
### What is the recipient address?-
### Felix@letsdefend.io
### Is the mail content suspicious?-yes
### Are there any attachment?-Yes
### Lets Start the Playbook
<img width="1558" height="528" alt="image" src="https://github.com/user-attachments/assets/43838b6b-fe7f-411d-b7d3-e9b966de2984" />

### Lets check if there is attachments and urls in the email
<img width="984" height="488" alt="image" src="https://github.com/user-attachments/assets/fe878737-9e3e-4f04-b9fb-f4d357eea42a" />

### Navigate to the email security tab and search for felix and look for the mail
<img width="1506" height="685" alt="image" src="https://github.com/user-attachments/assets/c00fdc79-c70b-4b25-8aeb-492e36e77d44" />

### There is url and attachment is available on the mail
<img width="1508" height="655" alt="image" src="https://github.com/user-attachments/assets/d96a9a83-ea44-4567-96f3-790a5596b8bc" />

### As you can see the Attachment is Password Protected 
### Phishing email attachments are often password-protected for several strategic reasons:
### - Bypass Security Filters: Many email security systems cannot scan encrypted or password-protected files, allowing malicious content to pass through undetected.
### - Avoid Antivirus Detection: Since the file is locked, antivirus tools cannot inspect its contents until it is opened by the user.
### - Increase Curiosity and Trust: Providing the password in the email makes the message appear more legitimate and intentional, encouraging the recipient to open it.

### Analyzing the Url and Attachment
<img width="981" height="567" alt="image" src="https://github.com/user-attachments/assets/3b62e765-25be-4874-8453-29be878eefa7" />

<img width="1898" height="918" alt="image" src="https://github.com/user-attachments/assets/4e6a28a1-f2b6-472c-98a9-853e81729374" />

### 14/95 Vendors are flagged url as malicious in Virus Total
### 11/95  Vendors are flagged Ip as malicous in  Virus Total
### Here are the details of Ip from shodan.io
<img width="1902" height="971" alt="image" src="https://github.com/user-attachments/assets/048afa35-e4a4-4853-85bb-5d98a4073e2b" />

### Analyzing the attachment coffee.exe inside the mail
### Always use sandbox to analyse the files
<img width="1100" height="1095" alt="image" src="https://github.com/user-attachments/assets/d2a02a33-2f5b-4360-b60e-fcdb0b646406" />

### Open network analysis tab to see contacted domains
<img width="1100" height="784" alt="image" src="https://github.com/user-attachments/assets/89494724-5b23-4347-aa31-b70ab8f7fcb8" />

### Use lets defend Threat Intelligence 
<img width="1473" height="250" alt="image" src="https://github.com/user-attachments/assets/4853cf08-49f2-4f91-9df4-405fe9c5488c" />

### After analysis both url and Attachment is Malicious 
<img width="986" height="573" alt="image" src="https://github.com/user-attachments/assets/8ddec508-4356-43a0-8a6c-20fae409816a" />

### Checking if the mail is delivered to user
<img width="997" height="393" alt="image" src="https://github.com/user-attachments/assets/f2579e9e-a54d-49a4-b01f-319be2c91904" />

### Yes, The action is "ALLOWED"
<img width="1438" height="146" alt="image" src="https://github.com/user-attachments/assets/7f2c6eb3-9638-4d5b-bf53-8d509f37dded" />

### Delete the mail
<img width="993" height="356" alt="image" src="https://github.com/user-attachments/assets/a21ff0c1-43bc-4f16-b139-7e6a6e79aa0e" />

### Navigate to the email security and search for felix
### Click delete button
<img width="1504" height="697" alt="image" src="https://github.com/user-attachments/assets/bb705a9a-1a92-4489-8680-eab4fc65a917" />

### Checking if someone received same url/attachment
<img width="996" height="499" alt="image" src="https://github.com/user-attachments/assets/fd8230eb-c558-49d3-a5d6-763ac95585db" />

### Navigate to the Log management and search for C2 connections for this Ip "37.120.233.226"
<img width="1498" height="719" alt="image" src="https://github.com/user-attachments/assets/a61d0d6f-7fbd-454e-a7ca-be5ec86bf1ad" />

### We can see two logs and both belongs to felix 172.16.20.151 
<img width="1499" height="542" alt="image" src="https://github.com/user-attachments/assets/7e3fd89e-4c0f-4b19-a291-a9c69334165d" />

### The file was opened and firewall permitted the connection The C2 connection is established 
### Since the file opened and connection established. Begin containment process
<img width="979" height="407" alt="image" src="https://github.com/user-attachments/assets/8be58c69-7628-4e02-89dd-276135f021b3" />

### Navigate to the Endpoint security and to felix machines
<img width="1275" height="447" alt="image" src="https://github.com/user-attachments/assets/d95381c5-79a6-4b89-bb37-ca07377ecdc0" />


### We can see the browser History the user felix  has accessed and opened the file
### Network Activity Tab shows a clear contact with C2 Ip address
<img width="1085" height="479" alt="image" src="https://github.com/user-attachments/assets/d4b5d60a-2895-41a6-b5d3-4a3dabc9c503" />

### Navigate to the Endpoint security and contain felix machines
<img width="1532" height="771" alt="image" src="https://github.com/user-attachments/assets/356ccaf3-0e27-4a58-955e-7c18d3a3b572" />

### Add Artifacts to the alert
<img width="975" height="788" alt="image" src="https://github.com/user-attachments/assets/38304261-0c20-4804-b16b-f4976e91d60c" />

### We have completed the playbook
<img width="982" height="350" alt="image" src="https://github.com/user-attachments/assets/52b335eb-618b-4e47-a207-180a07f106d6" />

## Congratulations !!! We have Successfully Investigated this Alert
<img width="1394" height="524" alt="image" src="https://github.com/user-attachments/assets/b36cf29b-6554-402d-a460-62d111d305cf" />




















































