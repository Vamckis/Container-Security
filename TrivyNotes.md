# To scan Docker images which are already installed:
%docker images
% trivy image <image name>

# To Scan Dockerfile which is not pulled into docker:
% trivy config <dir name of folder containing Dockerfile>

# To Scan all Docker files in a directory:
% trivy fs <dir name of folder conataining all folders>

% trivy fs --security-checks vuln,config Docker-Images