                                **Packet Investigation and Analysis Lab**

This lab focuses on packet investigation and network traffic analysis using the packet capture dataset created from my personal MacBook Pro. In this lab phase, the goal is to move beyond basic log review and begin analyzing real packet-level traffic. This lab helps to understand how devices communicate across the network, what IP addresses are involved, which protocols are being used, and whether any traffic patterns look unusual or suspicious.
In this lab, the main tool we start with is tcpdump, especially the command tcpdump -r network_capture.pcap, which reads an existing packet capture file instead of capturing live traffic. Later, the same PCAP file can be analyzed with Wireshark for graphical packet inspection, Zeek for structured network logs, and Suricata for IDS-style detection and alerting. These tools are commonly used by SOC analysts, network defenders, malware analysts, and incident responders to investigate network behavior.
During this lab, the packet capture will be analyzed for source IPs, destination IPs, protocols, DNS requests, TLS/HTTPS traffic, and suspicious communication patterns. The purpose is to identify who the MacBook Pro communicated with, what type of traffic was generated, whether DNS or encrypted traffic appears in the capture, and whether any repeated or unusual connections should be investigated further. This lab builds practical packet analysis skills and prepares the dataset for later investigation in Wireshark, Zeek, Suricata, and Splunk.

**Step 1 — Navigate to Dataset Folder**

Command: cd ~/Downloads

Command: ls

Locate the packet capture dataset.

Please refer to image # 1 in the repository 


**Step 2 — Verify Packet Capture File Exists**

Command: ls -lh *.pcap

verify the PCAP dataset exists

confirm packet capture file size.

Please refer to image # 2 in the repository.



**Step 3 — Read Packet Capture File**

Command: tcpdump -r mac_network_capture.pcap

read packet capture dataset, 

display packet-level traffic. 

Please refer to image # 3




**Step 4 — Display First 20 Packets**

Command: tcpdump -r mac_network_capture.pcap | head -20

review beginning of packet capture, 

identify source/destination communication. 

Please refer to image # 4




**Step 5 — Analyze Source and Destination IPs**

Command: tcpdump -r mac_network_capture.pcap | awk '{print $3, $5}' | head

identify communication pairs, 

analyze source → destination traffic. 

IP communication pairs screenshot

Please refer to images # 5 in the repository.

 


**Step 6 — Extract Unique Source IPs**

Command: tcpdump -r mac_network_capture.pcap | awk '{print $3}' | sort | uniq

identify unique traffic sources. 

Please refer to image # 6

 

**Step 7 — Extract Unique Destination IPs**

Command: tcpdump -r mac_network_capture.pcap | awk '{print $5}' | sort | uniq

identify external destinations, 

analyze remote systems.

Please refer to image # 7
 



**Step 8 — Analyze HTTPS/TLS Traffic**

Command: tcpdump -r mac_network_capture.pcap | grep "443"

identify encrypted HTTPS/TLS communication, 

analyze secure web traffic. 

Please refer to image # 8




**Step 9 — Analyze DNS Traffic**

Command: tcpdump -r mac_network_capture.pcap | grep "53"

Purpose:

investigate DNS requests, 

identify domain resolution activity. 

Please refer to image # 9
 



**Step 10 — Count Packets in Capture**

Command: tcpdump -r mac_network_capture.pcap | wc -l

determine total packet volume.

Please refer to image # 10

 


**Step 11 — Identify Most Frequent Communication**

Command: tcpdump -r mac_network_capture.pcap | awk '{print $5}' | sort | uniq -c | sort -nr | head

identify most contacted remote systems, 

detect repeated communication patterns.

Please refer to image # 11
 



**Step 12 — Save DNS Investigation Dataset**

Command: tcpdump -r mac_network_capture.pcap | grep "53" > dns_traffic.log

create DNS investigation dataset. 

Command: ls -lh dns_traffic.log

Please refer to image # 12


 


**Step 13 — Save TLS Investigation Dataset**

Command: tcpdump -r mac_network_capture.pcap | grep "443" > tls_traffic.log

create TLS/HTTPS investigation dataset. 

Command: ls -lh tls_traffic.log

Please refer to image # 13


 


**Step 14 — Create Suspicious Communication Dataset**

Command: tcpdump -r mac_network_capture.pcap | awk '{print $3, $5}' | sort | uniq -c | sort -nr > suspicious_connections.log

create communication analysis dataset, 

identify repeated/suspicious traffic patterns. 

Command: head suspicious_connections.log

Please refer to image # 14


 



**Step 15 — Review Generated Investigation Datasets**

The Step 15  Review Generated Investigation Datasets is now successfully completed.

Output confirms all three datasets were created:

dns_traffic.log              544B
suspicious_connections.log   437B
tls_traffic.log               20K


dns_traffic.log — contains DNS-related packet activity extracted from the PCAP. 
tls_traffic.log — contains HTTPS/TLS and QUIC traffic over port 443 extracted from the PCAP. 
suspicious_connections.log — contains communication patterns and repeated source/destination pairs used for threat-hunting analysis. 


This step verified that all investigation datasets were successfully generated from the packet capture file. The DNS, TLS, and suspicious communication datasets were reviewed to confirm successful creation and availability for future packet analysis, threat hunting, network monitoring, and SOC investigation activities.

Packet Investigation and Analysis Lab is now complete.

**lab folder on the personal macbook pro containing**:

mac_ifconfig.log

mac_netstat.log

listening_ports.log

mac_network_capture.pcap

dns_traffic.log

tls_traffic.log

suspicious_connections.log

These datasets can later be used for:

Wireshark analysis
 
Zeek network monitoring
 
Suricata IDS analysis
 
Splunk ingestion and dashboards
 
Additional threat hunting exercises
 


