 Phase 1 – Enumeration
 platform: Hack the Box
Network Scan

Command:

nmap -sV  <10.129.1.160>


Purpose:
To identify open ports, services, versions and potential vulnerabilities.

<img width="887" height="533" alt="image" src="https://github.com/user-attachments/assets/01c6228b-1d27-447d-af97-e8f73823edcb" />

🖥 Lab: SMB Enumeration & Share Access

Platform: Hack The Box
Objective: Enumerate SMB shares and access restricted content

🎯 Objective

Identify available SMB shares

Authenticate as user bob

Access the flag directory

Retrieve contents of flag.txt

🔎 Phase 1 – SMB Share Enumeration
Command Used

nmap --script smb-os-discovery.nse -p445 10.129.1.160

<img width="856" height="312" alt="image" src="https://github.com/user-attachments/assets/5b3d246c-0a6d-472d-b5ae-37bab8df3b4a" />

nmap -A -p445 10.129.1.160

<img width="895" height="528" alt="image" src="https://github.com/user-attachments/assets/b307e45a-8fd8-4a79-9d5d-c400a24c4706" />

<img width="875" height="603" alt="image" src="https://github.com/user-attachments/assets/ead5c4df-8632-4c6f-a1b5-a43aec3afe1b" />
Breakdown of the Command

-A → Enables:

OS detection

Version detection

Script scanning

Traceroute

-p445 → Scans only port 445 (SMB)

10.129.1.160 → Target IP address

Purpose

To perform in-depth enumeration of the SMB service running on port 445 and gather information about:

Operating system

SMB version

Host details



