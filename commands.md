alert tcp any any -> $HOME_NET any (msg:"[LAB] Possible SYN Port Scan"; flags:S; threshold:type threshold,track by_src,count 20,seconds 5; sid:100001;)
alert icmp any any -> $HOME_NET any (msg:"[LAB] ICMP Flood Detected"; threshold:type threshold,track by_src,count 50,seconds 5; sid:100002;)
alert udp any any -> any 53 (msg:"[LAB] DNS Query to Malicious Domain"; content:"malicious"; nocase; sid:100005;)
alert tcp $HOME_NET any -> any $HTTP_PORTS (msg:"[LAB] Malware .exe Download"; content:".exe"; http_uri; sid:100004;)

from scapy.all import rdpcap
from collections import Counter

packets = rdpcap("attack.pcap")
syn = sum(1 for p in packets if p.haslayer('TCP') and p['TCP'].flags=='S')
icmp = sum(1 for p in packets if p.haslayer('ICMP'))
print(f"SYN packets: {syn} -> {'Port Scan!' if syn>50 else 'Normal'}")
print(f"ICMP packets: {icmp} -> {'Flood!' if icmp>100 else 'Normal'}")
print(f"Top Talkers: {Counter([p['IP'].src for p in packets if p.haslayer('IP')]).most_common(3)}")

#!/bin/bash
sudo tcpdump -i eth1 -w pcaps/attack.pcap -G 60 -W 1