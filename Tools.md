## Docker Security Tools

### Trivy

### Dive
- A tool for exploring a docker image, layer contents, and discovering ways to shrink the size of your Docker/OCI image.
- https://github.com/wagoodman/dive
### Dockscan
- https://github.com/kost/dockscan/
### Dockerlint
### Halolint
### Docker-bench-Security
- CIS Benchmarks

### Check Capabilities of Docker
- install libcap2-bin utility to know the capabilities available on the connected container
  - apt-get install libcap2-bin
- capsh command is part of the package libcap2-bin upon executing list the capabilities available on the container
  - capsh --print

### Nmap

### Pentesting
- list all repositories in container using curl
  - curl http://192.168.5.6:5000/v2/_catologue
  - curl http://:5000/v2/flag/tags/list
  - curl http://192.168.5.6:5000/v2/treasure-love/manifests/latest
  - curl http://192.168.5.6:5000/treasure-love/blobs/layername --output.tar
