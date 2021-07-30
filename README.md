# Container-Security
Includes Security Testing detail of Docker Container

# To Install Vulnerable Docker image:
$ docker pull nginx

# To Install Trivy in Mac:
% brew install aquasecurity/trivy/trivy

# To install Trivy in Debian:
$ sudo apt-get install trivy

# To scan Docker images which are already installed:
% docker images<br/>
% trivy image {image name}

# To Scan Dockerfile which is not pulled into docker:
% trivy config {dir name of folder containing Dockerfile}

# To Scan all Docker files in a directory:
% trivy fs {dir name of folder conataining all folders}

# References:
https://github.com/aquasecurity/trivy
