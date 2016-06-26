# Docker environment for python scripts
This is a base template for python in docker.
The purpose of this repository is to make it easy to create, build and deploy python scripts with docker.

The container set is based on the official [python:3-onbuild](https://hub.docker.com/_/python/) image.

## Configuration
Put all your python module dependencies in the `requirements.txt` file. The dependencies will then be installed at build. All files in the same folder as the Dockerfile will be copied into `/usr/src/app` by the python base image.

Modify the `docker-compose.yml` and `Dockerfile` to your likings to configure exposed ports, volume mounts, extra files, scripts etc.

## Using the image in development
To not have to rebuild the container each time you have updated your code. If you are using docker-compose, you can run the command:
```
docker-compose build dev && docker-compose run --rm dev bash
```
This will build a docker image and with the dependencies in the requirements.txt file, and then run the container with the console attached.

If you are using the image with pure docker, you can use the following commands:
```
docker build -t my-python-app .
docker run -it --rm -v "$PWD:/usr/src/app my-python-app bash"
```

Note that you can also install the dependencies in `requirements.txt` after you entered the container.

## Using the image in production
When the code is ready for production, remove the "dev" part in the docker-compose.yml file and do a:
```
docker-compose build
docker-compose up -d
```
