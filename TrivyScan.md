# Container-Security
Includes Security Testing details of Docker Images

### Demo test Apps
To Install Vulnerable Docker image: <br/>
$ docker pull nginx

### Trivy Installation: 
- In Mac: ``` % brew install aquasecurity/trivy/trivy ``` 
- In Debian: ``` $ sudo apt-get install trivy```
- In Windows: {Need to do research - No default options available for now}
- Note: Trivy has an disadvantage with report creation.

### To see Docker images which are already installed:
```% docker images```
``` % trivy image {image name} ```
- eg: trivy image nginx

### To Scan single Dockerfile:
``` % trivy config {dir name of folder containing Dockerfile} ```
- eg: trivy config python-2.7

### To Scan all Dockerfiles in a directory:
``` % trivy fs {dir name of folder conataining all folders} ```
- eg: trivy fs --security-checks vuln,config Demo-Docker-Images

### To Scan Github Repository:
``` % trivy repo {Github Repo URL} ```
- eg: trivy repo https://github.com/Vamckis/Container-Security

### To Output the trivy results into text file
``` % trivy image nginx > Output.txt```

### References:
https://github.com/aquasecurity/trivy
