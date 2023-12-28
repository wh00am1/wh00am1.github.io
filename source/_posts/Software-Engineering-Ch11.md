---
title: Software Engineering::Ch11
date: 2023-12-11 12:47:21
tags: 
    - notes
    - software engineering
---

## Architectural design decisions
- Static strutural model
- Dynamic process model
- Interface model
- Relationship model
- Distribution model
## System organisation
- Repository model
    - Shared data : in database
    - Sub-system : hold a database
    - Effective
    - Data manipulation centralize
    - Difficult evolution
    - Conflict policies between sub-systems
- Client-server model
    - Server & client
    - Network
    - Distributed archtecture
    - Easy to integrate
    - May change when adding
    - May be no shared data
    - Performance issue
- Layered model
    - Config management layer
    - Object management layer
    - DB system layer
    - OS layer
## Modular decomposition syles
- Sub-system : independent operator
- Module : system component, composed from others
- Decomposing strategies : 
    - Object-oriented
    - Function-oriented
## Control styles
- Centralised control
    - Call-ret model
    - The manager model
- Evend-based control
    - Broadcast models
    - Interrupt-driven models
## Reference architectures
- OSI
- ECMA (for CASE env)
