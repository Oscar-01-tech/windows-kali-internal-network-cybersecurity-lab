# windows-kali-internal-network-cybersecurity-lab
Hands-on cybersecurity lab using Windows 11 Pro and Kali Lnux to configure internal networking, enable RDP, and perform Nmap scanning and service enumeration.

This project demonstrates a virtualized cybersecurity lab environment using Windows 11 Pro as the target system and Kali Linux as the attacker system. The goal was to configure internal networking between both machines, enable a remote service on Windows, and perform Nmap scanning from Kali to enumerate open ports and verify connectivity.


**Project Objectives**

Build two virtual machines in VirtualBox

Configure an isolated internal network for secure communication

Create a Windows 11 local account (bypassing Microsoft account requirement)

Assign static IP addresses to both VMs

Verify connectivity using ping

Enable Remote Desktop Protocol (RDP) on Windows

Perform Nmap scanning from Kali to identify open ports

Troubleshoot filtered ports and firewall rules


**Virtual Machine Setup**

Windows 11 VM
Static IP: 192.168.10.10

Subnet mask: 255.255.255.0

Verified using ipconfig

Kali Linux VM
Static IP: 192.168.10.11/24

Commands used:

Code
sudo ip addr add 192.168.10.11/24 dev eth0
sudo ip link set eth0 up
VirtualBox Network Configuration
### VirtualBox Internal Network Settings
![VirtualBox network settings](screenshots/<img width="1919" height="1079" alt="Screenshot 2026-01-30 171717" src="https://github.com/user-attachments/assets/ade1abde-faf6-4386-85df-f976e6d33bfb" />
.png)
Adapter: Internal Network

Network name: labnet

Adapter type: Intel PRO/1000 MT Desktop

Cable connected: Enabled


**Windows 11 Configuration**

Local Account Creation
Windows 11 attempted to force a Microsoft account during setup. A local account was created using offline setup methods to ensure the VM remained isolated and usable for internal‑only testing.

Network Verification
ipconfig confirmed the assigned static IP and interface configuration.
###  Windows Static IP Configuration (192.168.10.10)
![Windows static IP](screenshots/<img width="1030" height="766" alt="Screenshot 2026-01-30 162516" src="https://github.com/user-attachments/assets/f51c0146-6a1a-46c4-b07d-cddc14797783" />
.PNG)

Enabling Remote Desktop
Remote Desktop enabled

Network Level Authentication enabled

Remote Desktop Services set to Running and Automatic

Firewall Configuration
Inbound rules enabled:

Remote Desktop (TCP)

Remote Desktop (UDP)

Remote Desktop Shadow (TCP)

Service Verification
netstat -an | find "3389" confirmed:

TCP 3389 listening

UDP 3389 listening


**Kali Linux Configuration**
### Kali Static IP Configuration (192.168.10.11)
![Kali static IP](screenshots/<img width="1918" height="1075" alt="Screenshot 2026-01-30 165833" src="https://github.com/user-attachments/assets/930bb735-e650-44b1-82d1-43a1b34d9fd5" />
)

Network Verification
ip addr confirmed:

lo loopback

eth0 with 192.168.10.11/24

Connectivity Testing
Ping tests:

Kali → Windows: 0% packet loss

Windows → Kali: 0% packet loss

This verified that both VMs were communicating correctly on the internal network.


**Nmap Scanning**

Initial Scan
Code
nmap -sV 192.168.10.10
Early scans showed:

All 1000 ports filtered

No responses from Windows

After Enabling RDP
A later scan revealed:

3389/tcp OPEN

Service detected: ms-wbt-server (Remote Desktop Protocol)

This confirmed:

Windows firewall rules were correct

RDP was active

The internal network was functioning as intended


**Troubleshooting Summary**

Windows initially showed “media disconnected” due to adapter configuration

Kali required manual IP assignment using ip addr add

Early Nmap scans showed all ports filtered

Windows firewall rules were adjusted to allow RDP

Verified open port 3389 using both Nmap and netstat

Confirmed bidirectional connectivity with ping tests


**Final Results**

Both VMs successfully communicated over an isolated internal network

Windows RDP service was exposed and detected by Kali

Nmap enumeration successfully identified open ports

The lab environment is fully functional and reproducible


**Project Summary**

Cybersecurity Virtual Lab Project — Windows 11 & Kali Linux

Built a virtualized cybersecurity lab using VirtualBox with Windows 11 as the target and Kali Linux as the attacker

Configured internal networking and static IP addressing for cross‑VM communication

Enabled and verified Windows Remote Desktop Protocol (RDP) using firewall rules and netstat

Performed Nmap scanning and service enumeration from Kali to identify open ports

Documented troubleshooting steps including network configuration, filtered ports, and Windows account setup.
