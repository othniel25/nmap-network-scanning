 Enumeration
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

smbclient -N -L \\\\10.129.1.160
<img width="870" height="441" alt="image" src="https://github.com/user-attachments/assets/ea88f73f-128e-4eed-8e78-368cfab8ecb9" />

Breakdown:

-N → No password (anonymous login)

-L → List available shares

\\10.129.1.160 → Target host
Findings

Discovered three shares: print$, users, and IPC$

Anonymous authentication allowed share listing

SMBv1 negotiation failed

Security Analysis

The failure to negotiate SMBv1 suggests that the server has deprecated the insecure SMBv1 protocol and likely supports SMBv2 or SMBv3 instead. This reduces exposure to legacy SMB vulnerabilities such as MS17-010 (EternalBlue).

However, the ability to list shares anonymously increases the attack surface and may allow further enumeration.

smbclient -U bob \\10.129.1.160\users

<img width="876" height="573" alt="Screenshot 2026-02-11 235148" src="https://github.com/user-attachments/assets/19df3124-96da-4230-abdf-95e00deb9acb" />
<img width="884" height="376" alt="Screenshot 2026-02-11 235220" src="https://github.com/user-attachments/assets/f9fd0420-2e8b-49b4-a49a-df2d08b622c3" />

🔎 Findings

While enumerating the users SMB share as user bob, I identified a directory structure containing user-specific folders. Within Bob’s directory, a file named passwords.txt was discovered and successfully retrieved.

🌐 Web Enumeration Phase

Directory Brute Force

I performed directory brute-forcing to discover hidden files and directories that might lead to an entry point or sensitive information.

Tool: Gobuster
<img width="867" height="615" alt="Screenshot 2026-02-12 084235" src="https://github.com/user-attachments/assets/22f99cf7-b5d1-4cb2-8ebc-5c70c834a5f8" />
<img width="866" height="466" alt="Screenshot 2026-02-12 084327" src="https://github.com/user-attachments/assets/c7634e36-2e59-4217-9609-225d05a9a460" />

Purpose

To discover hidden directories and web application endpoints.

The presence of an exposed login page suggests potential for credential-based access, especially when combined with credentials discovered via SMB enumeration.
