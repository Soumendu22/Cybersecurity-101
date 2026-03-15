# Packet Analysis

- Packet Concept
    
    - Small unit of network data
        
    - Contains header and payload
        
    - Used for communication
        
- Packet Structure
    
    - Header
        
        - Source IP
            
        - Destination IP
            
        - Protocol
            
    - Payload
        
        - Actual transmitted data
            
- Network Layers
    
    - Application
        
    - Transport
        
    - Network
        
    - Data Link
        
    - Physical
        
- Packet Capture Tools
    
    - Wireshark
        
    - tcpdump
        
    - Tshark
        
    - Zeek
        
    - NetworkMiner
        
- tcpdump Commands
    
    - Capture interface
        
        - tcpdump -i eth0
            
    - Filter by port
        
        - tcpdump port 80
            
    - Filter by IP
        
        - tcpdump host 192.168.1.1
            
    - Save capture
        
        - tcpdump -w capture.pcap
            
- Wireshark Filters
    
    - ip.addr == 192.168.1.1
        
    - tcp.port == 80
        
    - dns
        
    - http
        
    - tcp
        
- Common Protocols
    
    - HTTP
        
    - HTTPS
        
    - DNS
        
    - TCP
        
    - UDP
        
    - ICMP
        
- Cybersecurity Use
    
    - Detect malware traffic
        
    - Investigate attacks
        
    - Monitor network
        
    - Forensics analysis
        
- Suspicious Indicators
    
    - High traffic
        
    - Unknown IP connections
        
    - DNS anomalies
        
    - Reverse shell traffic