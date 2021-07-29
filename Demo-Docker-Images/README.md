# Python CI Docker images

This repository contains Docker images for Python which are based on the [official Python Docker images](https://hub.docker.com/r/_/python/). These images were created specifically to use them for continious integration (Gitlab CI specifically), but they can be used for other purposes too.

## Pull images

The images are stored on [Docker Hub](https://hub.docker.com/r/geertw/docker-python-ci/). Use `docker pull geertw/docker-python-ci` to pull these images.

Available tags:

* `2.7`, `2.7-alpine`
* `3.3`, `3.3-alpine`
* `3.4`, `3.4-alpine`
* `3.5`, `3.5-alpine`

The alpine images are smaller. The normal images also contain a MySQL client for database interaction.

## Build process

The Dockerfiles are stored in directories for each image version. Docker Hub builds new images automatically when this repository or the Python base images are updated.

## License

The Dockerfiles are licensed under the MIT license, see LICENSE for details.

