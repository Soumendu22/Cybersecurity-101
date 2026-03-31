# SSRF

- SSRF Concept
    
    - server makes attacker-chosen requests
    
- High-Risk Targets
    
    - localhost/internal services
    
    - cloud metadata endpoints
    
- Defenses
    
    - strict host allowlist
    
    - DNS and redirect validation
    
    - block internal/link-local ranges
    
    - egress filtering
