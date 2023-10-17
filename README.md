# Container-Security (Docker & Kubernetes)
## Docker: OWASP Top 10
<details> 
<summary> 1: Host OS Vulnerabilities</summary>
- If Host OS have vulnerabilities, attacker can use it to gain access to containers and apps running inside them.
- Example: CVE-2016-5195 - Dirty COW Vulnerability - Privilege escalation in Linux kernel.
- Attacker an gain root access using the Dirty COW Vulnerability.
- Resolution: Regular patching of host OS, Usage of IDS, Firewall, Implement strict access controls

#### CVE-2021-42013 (Path Traversal + RCE + Reverse Shell Attack)
- An attacker could use a path traversal attack to map URLs to files outside the directories. If files outside of these directories are not protected by the usual default configuration "require all denied", these requests can succeed. If CGI scripts are also enabled for these pathes, this could allow for remote code execution.
- This issue affects Apache 2.4.49 and Apache 2.4.50 and not earlier versions.
- Path Traversal payload - ``` http://172.17.0.2:80/cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/etc/passwd ```
- Actual payload After double URL decode - ``` http://172.17.0.2:80/cgi-bin/../../../../../../../etc/passwd ```
- References: https://github.com/twseptian/cve-2021-42013-docker-lab
</details>
