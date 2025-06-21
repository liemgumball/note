---
Created: 2024-09-24T11:55
Class: mgm
Type: Security
Reviewed: false
Edited: 2024-10-16T22:39
---
> [!important] Our computer is liked a castle

![[Screenshot_2024-09-24_at_11.56.53.png]]

The wall and gates is TCP protocol, only 2 gates are opened.

- 80: http
- 443: https

> [!important] Web application is insecure by default. Developers have to guarantee their web application’s security on their own.

## Malware

==Mal==icious soft==ware==

- Worm: malware that replicates itself, automatically spreading through a network
- Ransomware: encrypt files in our computer and requires money to decrypt
- Botnet: a network of computer used to launch a cyber attack (DDoS attack)

## Data leakage

- Side channel: attacker places probes ⇒ often requires physical proximity
- Covert channel: info leak over channels not intended for communication
- Steganographic channel

  

![[Screenshot_2024-09-30_at_16.13.55.png]]

![[Screenshot_2024-09-30_at_16.15.18.png]]

![[Screenshot_2024-09-30_at_16.25.50.png]]

  

## Sensitive Data

![[Screenshot_2024-10-01_at_11.36.04.png]]

It can be leak in many place

- referrer-header
- referrer-policy
- caching
    - vary (difference based on device)
    - max-age
    - no-cache
    - no-store

![[Screenshot_2024-10-01_at_14.24.49.png]]

# Cross-site Request Forgery (CSRF)

# Origin and Public Suffix

  

![[Screenshot_2024-10-07_at_23.07.07.png]]

# Session Riding attacks

![[Screenshot_2024-10-16_at_22.38.29.png]]