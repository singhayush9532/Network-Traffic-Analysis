## Part 1: Setup tcpdump
sudo apt install tcpdump wireshark snort -y
sudo tcpdump -i eth1 -w attack.pcap

## Part 2: Wireshark Filters (Use these for screenshots)
tcp.flags.syn==1 && tcp.flags.ack==0  # Detects SYN Scan
icmp  # Detects ICMP Flood
dns.qry.name.len > 40  # Detects DNS Tunneling
http contains ".exe"  # Detects Malware Download

## Part 3: Snort Rules
Copy rules/local.rules to /etc/snort/rules/
Run: sudo snort -c /etc/snort/snort.conf -A console -r attack.pcap

## Part 4: Simulate Attack (From Kali)
nmap -sS 192.168.56.104
ping -f 192.168.56.104 (for 10 sec)
nslookup very-long-suspicious-domain-for-tunneling-test.malicious.com
curl -A "MalwareDownloader/1.0" http://192.168.56.104/malware.exe