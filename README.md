# Container-Security
Includes Security Testing detail of Docker Container

# Demo test Apps
To Install Vulnerable Docker image: <br/>
$ docker pull nginx

# Trivy Installation 
In Mac: <br/>
% brew install aquasecurity/trivy/trivy

In Debian: <br/>
$ sudo apt-get install trivy

In Windows: <br/>
{Need to do research - No default options available for now}

# To scan Docker images which are already installed:
% docker images<br/>
% trivy image {image name} <br/>
eg: trivy image nginx

# To Scan single Dockerfile:
% trivy config {dir name of folder containing Dockerfile} <br/>
eg: trivy config python-2.7

# To Scan all Dockerfiles in a directory:
% trivy fs {dir name of folder conataining all folders} <br/>
eg: trivy fs --security-checks vuln,config Demo-Docker-Images

# To Scan Github Repository:
% trivy repo {Github Repo URL} <br/>
eg: trivy repo https://github.com/Vamckis/Container-Security

# References:
https://github.com/aquasecurity/trivy
