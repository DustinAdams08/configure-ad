<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Make a Resource Group and a Virtual Machine (VM)
- Step 2: Make a Virtual Network and Subnet
- Step 3: Create the Domain Controller VM (Windows Server 2022)
- Step 4: Create Client VM (Windows 10)
- Step 5: Install Active Directory Role
- Step 6: Promote to Domain Controller
- Step 7: Set Domain Name
- Step 8: Restart VM
- Step 9: Test It by logging in with new domain and create test users

<h2>Deployment and Configuration Steps</h2>


Step 1. Create a Resource Group 
•	Name it Active-Directory
•	Region: US Central US

![image](https://github.com/user-attachments/assets/05b478f3-9f86-425e-8bc7-91ce5859a2af)

Step 2. Create a Virtual Network
•	Type Virtual Network
•	Resource Group: Put it in Active Directory
•	Virtual Network Name: Active Directory-vnet 
•	Then click Review & Create

![image](https://github.com/user-attachments/assets/12d1705c-faab-46df-8ae6-ec1d76a2bc8b)

Step 3. Create a Virtual Machine 
•	Type: Virtual Machine, and then click Create New VM
•	Resource Group: Active Directory
•	VM name: dc-1
•	Region: US Central US
•	Image: Windows Server 2022 
•	Size: Make sure it has 2 virtual CPUs
•	Username: labuser
•	Password: Cyberlab123!
•	Check the licensing box
•	Then click Review & Create

![image](https://github.com/user-attachments/assets/d2c31d30-81d9-4db3-a8c4-717fa1a1661e)
![image](https://github.com/user-attachments/assets/361fa704-4e21-49c2-85fe-e2d9ddfdce65)

Step 4. Create a Virtual Machine
•	Type: Virtual Machine, and then click Create New VM
•	Resource Group: Active Directory
•	VM name: Client-1
•	Region: US Central US
•	Image: Windows 11 Pro 
•	Size: Make sure it has 2 virtual CPUs
•	Username: labuser
•	Password: Cyberlab123!
•	Check the licensing box
•	Then click Review & Create

![image](https://github.com/user-attachments/assets/614df52c-34c8-475e-a98c-20389cfe2d33)


Step 5. Set the Domain Controller’s NIC Private IP address to be static
•	Click into VM dc-1
•	Click on network settings
•	Click on the NIC – Virtual Network Interface Card

![image](https://github.com/user-attachments/assets/dd9066f5-1d6b-42ee-909d-df08ea598225)
![image](https://github.com/user-attachments/assets/933d036e-d5ab-4380-b772-4387220d8309)

Step 6. Log in to the VM and Disable the Windows Firewall
•	This is to test connectivity
•	Get dc-1 Public IP address

![image](https://github.com/user-attachments/assets/29eb30b7-4ca9-4485-ab51-7013f54852ca)
![image](https://github.com/user-attachments/assets/78bb0316-6578-4b77-b717-a412bb6117be)

•	Enter the Username: labuser
•	Password: Cyberlab123!
•	Get logged in to the Domain Controller

![image](https://github.com/user-attachments/assets/2581e0e3-55b4-437d-90a7-f268840f2ab7)

•	Right-click the Start menu, click Run
•	Type wf.msc
•	Then click Windows Defender Firewall Properties 

![image](https://github.com/user-attachments/assets/d64a80fa-66d7-4efa-9324-e6629bc5ca49)

•	Under Firewall State, turn it off
•	Under Private Profile, turn it off
•	Under Public Profile, turn it off
•	Then click ok

![image](https://github.com/user-attachments/assets/d6f0a6d8-d53a-4acd-89d4-173c438e4cca)

Step 7. Set Client-1’s DNS settings to DC-1’s Private IP address
•	Find DC-1’s Private IP address
•	Click Virtual Machines – the DC-1

![image](https://github.com/user-attachments/assets/7b00a89a-7a5b-4f5b-9b18-d5a66677ac92)

•	Go to the Client-1 VM
•	Go to Network Settings
•	Click on Client-1 NIC

![image](https://github.com/user-attachments/assets/498f3301-04b6-45be-9fa4-9a833168ecfa)

•	Click On DNS Servers
•	Then paste the Private IP Address for dc-1 VM
•	Then Click Save

![image](https://github.com/user-attachments/assets/b0f257db-b718-4e29-a2b9-1437e16036d7)

Step 8. Restart Client-1 VM
•	Type Virtual Machines – then select the Client-1 VM box and click Restart

![image](https://github.com/user-attachments/assets/42c049a0-2102-4c43-92e5-e869d4c379e8)

Step 9. Log in to VM Client-1 and Ping dc-1’s private address
•	Start by getting Client-1’s public IP address
•	This can be found on VM’s homepage 

![image](https://github.com/user-attachments/assets/a808ce72-b168-41dd-8045-07b6b5feecd8)

•	Then go to Remote Desktop and enter the IP Address
•	Enter the Username: labuser
•	Password: Cyberlab123!
•	Get logged in to the VM and accept
•	Then get dc-1’s Private IP address under Overview

![image](https://github.com/user-attachments/assets/d1d6b2d0-0946-43fc-b61e-84d643da3349)

Step 10. Open PowerShell in Client-1
•	Click Start and type PowerShell

![image](https://github.com/user-attachments/assets/232803ec-5297-48e0-b63d-7bdc0572c07b)

•	Then type ping 10.0.0.4

![image](https://github.com/user-attachments/assets/0880d068-1cf0-4de1-b871-da321901c2bf)

•	Then we run ipconfig /all
•	The output for the DNS setting will show dc-1’s private IP Address

![image](https://github.com/user-attachments/assets/a15f6083-78fb-498f-be84-f05549b69ad6)

