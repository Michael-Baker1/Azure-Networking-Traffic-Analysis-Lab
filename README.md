# Azure Networking & Traffic Analysis (Wireshark)

![Azure](https://img.shields.io/badge/Cloud-Azure-0078D4?logo=microsoft-azure&logoColor=white)
![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?logo=wireshark&logoColor=white)
![Windows](https://img.shields.io/badge/OS-Windows%2010-0078D6?logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/OS-Ubuntu-E95420?logo=ubuntu&logoColor=white)
![Networking](https://img.shields.io/badge/Focus-Network%20Traffic%20Analysis-2ea44f)

---

## Objective
I wanted to get hands-on with network traffic analysis in a real cloud environment. The goal in mind was to spin up Windows and Linux virtual machines in Azure, generate traffic between them, and analyze it using Wireshark. This helped me understand how protocols like ICMP, SSH, DHCP, DNS, and RDP behave in practice.

## Environment Setup
- **Platform:** Microsoft Azure  
- **Resources:**  
  - Resource Group  
  - Virtual Network (192.168.0.0/16) with Subnet (192.168.1.0/24)  
  - Windows 10 VM (to run Wireshark and act as client)  
  - Linux (Ubuntu) VM (to act as target server)  
- **Tools:**  
  - Microsoft Remote Desktop  
  - Wireshark (installed on Windows VM)  

## What I Did
### Part 1 – Creating the Environment
- Created a resource group in Azure.  
- Deployed a Windows 10 VM and Ubuntu VM into the same virtual network and subnet.  
- Configured authentication with username/password.  

### Part 2 – Observing ICMP Traffic
- Connected to the Windows VM via Remote Desktop.  
- Installed and launched Wireshark to start capturing packets.  
- Filtered for ICMP traffic.  
- Pinged the Ubuntu VM’s private IP from the Windows VM and observed request/reply packets in Wireshark.  
- Also pinged a public website (google.com) to compare external vs. internal traffic.  

### Part 3 – Firewall & Protocol Analysis
**ICMP Traffic with Firewall Rules**  
- Started a continuous ping from the Windows VM to the Ubuntu VM.  
- Disabled inbound ICMP traffic in the Ubuntu VM’s Network Security Group.  
- Observed packet loss in both the ping output and Wireshark.  
- Re-enabled ICMP and confirmed packets resumed successfully.  

**SSH Traffic**  
- Filtered for SSH traffic in Wireshark.  
- From the Windows VM, initiated an SSH connection to the Ubuntu VM using its private IP.  
- Observed encrypted SSH traffic while logging in and running commands.  
- Disconnected from SSH and noted the traffic stopped.  

**DHCP Traffic**  
- Filtered for DHCP in Wireshark.  
- From Windows PowerShell, ran `ipconfig /renew` to request a new IP.  
- Observed DHCP Discover/Offer/Request/Ack traffic in Wireshark.  

**DNS Traffic**  
- Filtered for DNS traffic.  
- Used `nslookup` to resolve domains like google.com and disney.com.  
- Observed DNS query and response packets in Wireshark.  

**RDP Traffic**  
- Filtered for RDP traffic (`tcp.port == 3389`).  
- Observed the continuous stream of packets even when not actively clicking inside the VM.  
- Learned that RDP constantly transmits data to maintain a live desktop stream.  

### Cleanup
- Closed Remote Desktop sessions.  
- Deleted the Azure resource group to remove all resources and avoid costs.  

## What I Learned
- How to capture and analyze network traffic with Wireshark in a cloud environment.  
- The role of ICMP, SSH, DHCP, DNS, and RDP in everyday networking.  
- How firewall rules directly affect packet flow and visibility.  
- How Azure networking components (NSGs, VMs, subnets) tie together.  

## Why This Matters
Understanding how traffic looks on the wire is critical for IT, networking, and security roles. This lab gave me real-world practice analyzing packets, troubleshooting connectivity, and seeing the effects of security rules — exactly the kind of work that comes up in help desk, sysadmin, and cybersecurity roles.  

---

## 📸 Sreenshots
- Azure Portal showing both VMs deployed in the same virtual network.  
<img width="1959" height="493" alt="use this one" src="https://github.com/user-attachments/assets/e310d3de-71c6-4d6b-a9c6-1cf6b0e6acc8" />


- Failed ping attempt before firewall changes.  
<img width="1860" height="988" alt="werwer" src="https://github.com/user-attachments/assets/e948797f-4ebc-4f45-9300-b6997afa24bd" />


- Successful ping reply after creating the ICMP rule, and Wireshark capture showing ICMP echo requests and replies.  
<img width="1626" height="956" alt="11" src="https://github.com/user-attachments/assets/434a1479-19b7-496a-b378-51c3ba1bd14b" />


- Wireshark view of SSH traffic during login, and Wireshark capture of DHCP traffic during `ipconfig /renew`.  
<img width="1872" height="1040" alt="13" src="https://github.com/user-attachments/assets/6bf0e4b8-3e14-496f-b88b-fb7c658b652c" />


- DNS query/response traffic for `disney.com`.  
<img width="1788" height="954" alt="14" src="https://github.com/user-attachments/assets/679a1c7a-14ef-4b33-90bd-7a49bf5a9f1c" />


- Continuous RDP traffic stream in Wireshark.
<img width="1517" height="868" alt="15 RDP=port 3389" src="https://github.com/user-attachments/assets/b4e607e5-dfd8-448a-bd27-4a2bd51fdd9e" />

  
****
