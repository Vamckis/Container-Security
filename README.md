# Container-Security (Docker & Kubernetes)
## Docker: OWASP Top 10
### 1: Host OS Vulnerabilities
- If Host OS have vulnerabilities, attacker can use it to gain access to containers and apps running inside them.
- Example: CVE-2016-5195 - Dirty COW Vulnerability - Privilege escalation in Linux kernel.
- Attacker an gain root access using the Dirty COW Vulnerability.
- Resolution: Regular patching of host OS, Usage of IDS, Firewall, Implement strict access controls
#### CVE-2021-42013
- 
