# Network Traffic Analysis Lab
Objective: Capture and analyze network traffic to identify unusual patterns, malware, or signs of an attack.
Tools: Wireshark, tcpdump, Snort
Skills: Packet sniffing, traffic analysis, malware detection

## Lab Environment (Your VirtualBox Setup)
- Host: Windows 10
- VM1 - Victim: Ubuntu 22.04 (IP: 192.168.56.104)
- VM2 - Attacker: Kali Linux (IP: 192.168.56.103)
- Network: Host-Only Adapter (vboxnet0) - Isolated & Safe

## Tasks Covered
1. tcpdump live capture
2. Wireshark filter analysis
3. Snort IDS custom rules
4. Attack simulation (Port Scan, ICMP Flood, DNS Tunneling, HTTP Malware)
5. Python automated detection

Full guide: See lab_manual.md
