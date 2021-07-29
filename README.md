# Container-Security
Includes Security Testing detail of Docker Container

To Install Vulnerable Docker image:
docker pull nginx

To Install Trivy in Mac:
%brew install aquasecurity/trivy/trivy

To install Trivy in Debian:
%sudo apt-get install wget apt-transport-https gnupg lsb-release
%wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
%echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
%sudo apt-get update
%sudo apt-get install trivy
