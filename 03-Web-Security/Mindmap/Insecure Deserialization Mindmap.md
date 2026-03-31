# Insecure Deserialization

- Core Risk
    
    - untrusted serialized objects processed
    
- Impact
    
    - object injection
    
    - RCE and auth bypass
    
- Defenses
    
    - avoid native object deserialization
    
    - enforce schema validation
    
    - signed payload integrity
    
    - type allowlists
