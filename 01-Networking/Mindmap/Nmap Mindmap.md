# Nmap

- Overview
    
    - Network scanning tool
        
    - Used for network discovery
        
    - Used in penetration testing
        
    - Open-source security tool
        
- Basic Syntax
    
    - nmap [scan type] [options] target
        
- Target Specification
    
    - Single Host
        
        - nmap 192.168.1.1
            
    - Multiple Hosts
        
        - nmap 192.168.1.1 192.168.1.2
            
    - IP Range
        
        - nmap 192.168.1.1-100
            
    - Subnet Scan
        
        - nmap 192.168.1.0/24
            
    - Scan from File
        
        - nmap -iL targets.txt
            
- Port Scanning
    
    - SYN Scan
        
        - nmap -sS target
            
    - TCP Connect Scan
        
        - nmap -sT target
            
    - UDP Scan
        
        - nmap -sU target
            
    - ACK Scan
        
        - nmap -sA target
            
    - FIN Scan
        
        - nmap -sF target
            
    - Xmas Scan
        
        - nmap -sX target
            
- Port Selection
    
    - Single Port
        
        - nmap -p 80 target
            
    - Port Range
        
        - nmap -p 1-1000 target
            
    - All Ports
        
        - nmap -p- target
            
    - Top Ports
        
        - nmap --top-ports 100 target
            
    - Fast Scan
        
        - nmap -F target
            
- Host Discovery
    
    - Ping Scan
        
        - nmap -sn 192.168.1.0/24
            
    - Skip Ping
        
        - nmap -Pn target
            
    - TCP SYN Ping
        
        - nmap -PS target
            
    - TCP ACK Ping
        
        - nmap -PA target
            
    - UDP Ping
        
        - nmap -PU target
            
- Service Detection
    
    - Version Detection
        
        - nmap -sV target
            
    - Aggressive Scan
        
        - nmap -A target
            
- OS Detection
    
    - nmap -O target
        
- NSE Scripts
    
    - Vulnerability Scan
        
        - nmap --script vuln target
            
    - HTTP Enumeration
        
        - nmap --script http-enum target
            
    - FTP Anonymous Check
        
        - nmap --script ftp-anon target
            
    - SMB OS Discovery
        
        - nmap --script smb-os-discovery target
            
- Timing Options
    
    - T0 Paranoid
        
    - T1 Sneaky
        
    - T2 Polite
        
    - T3 Normal
        
    - T4 Aggressive
        
    - T5 Insane
        
- Output Options
    
    - Normal Output
        
        - nmap -oN scan.txt
            
    - XML Output
        
        - nmap -oX scan.xml
            
    - Grepable Output
        
        - nmap -oG scan.gnmap
            
    - All Formats
        
        - nmap -oA scan
            
- Practical Pentesting Workflow
    
    - Basic Scan
        
        - nmap target
            
    - Service Scan
        
        - nmap -sV target
            
    - Full Port Scan
        
        - nmap -p- target
            
    - Script Scan
        
        - nmap -sC target
            
    - Complete Recon Scan
        
        - nmap -sC -sV -p- -T4 target
            
- Common Ports
    
    - 21 FTP
        
    - 22 SSH
        
    - 23 Telnet
        
    - 25 SMTP
        
    - 53 DNS
        
    - 80 HTTP
        
    - 443 HTTPS
        
    - 445 SMB
        
    - 3306 MySQL
        
    - 3389 RDP