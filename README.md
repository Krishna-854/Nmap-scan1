# Nmap-scan1
Authorized Nmap scans for discovering open ports
Installed Nmap for windows from https://nmap.org/ and started a TCP SYN scan using my local IP address and found some open ports
I found open ports are 135,139,445,1521
135 — RPC / Endpoint Mapper

Service: Windows RPC/DCOM (epmap).
Top risks: service enumeration, info disclosure, exploitable RPC/DCOM RCEs.
Attacker use: fingerprint Windows services, chain to SMB/RDP exploits for lateral movement.
Priority mitigations: block on perimeter, patch Windows, limit RPC to trusted subnets, enforce VPN/jump host for remote management.

139 — NetBIOS Session Service (SMB over NetBIOS)

Service: NetBIOS/legacy SMB transport.
Top risks: share enumeration, anonymous access, NTLM relay/credential harvesting, legacy protocol weaknesses.
Attacker use: list/mount shares, misuse writable shares, pivot laterally.
Priority mitigations: block from untrusted networks, disable NetBIOS over TCP/IP if not in use, disable SMBv1, lock down share ACLs.

445 — SMB / Microsoft-DS

Service: SMB/CIFS (file sharing, domain services).
Top risks: wormable RCEs (e.g., EternalBlue class), data exfil, NTLM relay, lateral movement.
Attacker use: exploit SMB RCEs, capture/relay credentials, drop ransomware on writable shares.
Priority mitigations: do NOT expose to Internet, patch now, disable SMBv1, require SMB signing/NTLMv2, limit access through firewall/VPN.

1521 — Oracle TNS Listener

Service: Oracle DB listener (TNS).
Top threats: service discovery, default/weak passwords, unpatched TNS/DB vulnerabilties → total DB compromise/data export.
Attacker exploitation: discover SIDs/services, brute-force or exploit DB CVEs, read data.
Priority mitigations: block the Internet, bind listener to private IP, patch Oracle, implement strong DB creds and least privilege, force VPN/bastion for DB access.
