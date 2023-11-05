---
title: Software Engineering::Ch3
date: 2023-10-27 11:50:49
tags: 
    - software engineering
    - notes
---

## Critical system
<!-- more -->
### Types
- Safety-critical
- Mission-critical
- Business-critical
### Failure
- hardware
- software
- human operators
## System dependability
### Principal dimensions
- Avalibility
    - Deliver when requested
- Reliability
    - Deliver as specified
- Safety
    - Deliver without catastophic failure
- Security
    - Ability to self-protect
### Other system properties
- Repaiability
- Maintainability
- Survivability
- Error tolerance(avoid)
## Avaliblity and reliability
### Failures
- System failure
    - Does not deliver
- System error
    - Unexpected behavior
- System fault
    - Charactaristic leads to error
- Human error/mistake
### Improve reliability
- Fault avoidance
- Fault detectin&removal
- Fault tolerance
### Failure detection
- Input & output set
## Safety
### Safety-critical systems
- Primary safety-critical software
    - e.g. embedded controller
- Secondary safety-critical software
    - e.g. medical DB
### Reliable and safety
- No specified behaviour for critical situations
- Hardware malfunction
- A set of correct input lead to malfunction
### Assure safety
- Hazard avoidance
    - Hazard : a condition with potential for accident
- Hazard detection & removal
- Damange limitation
## Security
### Self protection against
- Exposure
- Vulnerability
- Attack
- Threats
- Control
### Damage type
- DoS
- Corruption (program/data)
- Information disclosure
### Assure security
- Vuln avoidance
- Attack detection & neutualisation
- Exposure limitation
