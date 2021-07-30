# Container-Security
Includes Security Testing detail of Docker Container

# Demo test Apps
To Install Vulnerable Docker image: <br/>
$ docker pull nginx

# To Install Trivy in Mac:
% brew install aquasecurity/trivy/trivy

# To install Trivy in Debian:
$ sudo apt-get install trivy

# To Install Trivy in Windows:
{Need to do research - No default options available for now}

# To scan Docker images which are already installed:
% docker images<br/>
% trivy image {image name}

# To Scan Dockerfile:
% trivy config {dir name of folder containing Dockerfile}

# To Scan all Dockerfiles in a directory:
% trivy fs {dir name of folder conataining all folders}

# References:
https://github.com/aquasecurity/trivy
