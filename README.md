<h1 align="center">Buildpacks Example</h1>

## Table Of Contents

- [About the Project](#about-the-project)
- [Requirements](#requirements)
- [Building](#building)
- [Running](#running)

## About The Project

This repo serves as a minimal example reference on creating a FastAPI application container
with [Buildpacks](https://buildpacks.io/).

## Requirements

- [Docker >= 17.05](https://www.python.org/downloads/release/python-381/)
- [Pack](https://buildpacks.io/docs/tools/pack/)
- [Python >= 3.7](https://www.python.org/downloads/release/python-381/)

> **NOTE** - Run all commands from the project root

## Building

Building

Check which Buildpacks are available

```shell
pack builder suggest
Suggested builders:
	Google:                gcr.io/buildpacks/builder:v1      Ubuntu 18 base image with buildpacks for .NET, Go, Java, Node.js, and Python
	Heroku:                heroku/buildpacks:18              Base builder for Heroku-18 stack, based on ubuntu:18.04 base image
	Heroku:                heroku/buildpacks:20              Base builder for Heroku-20 stack, based on ubuntu:20.04 base image
	Paketo Buildpacks:     paketobuildpacks/builder:base     Ubuntu bionic base image with buildpacks for Java, .NET Core, NodeJS, Go, Ruby, NGINX and Procfile
	Paketo Buildpacks:     paketobuildpacks/builder:full     Ubuntu bionic base image with buildpacks for Java, .NET Core, NodeJS, Go, PHP, Ruby, Apache HTTPD, NGINX and Procfile
	Paketo Buildpacks:     paketobuildpacks/builder:tiny     Tiny base image (bionic build image, distroless-like run image) with buildpacks for Java Native Image and Go
```

For this example we use the default Heroku-20 stack

> Note: In a real world setup you may want to use a custom builder tailored for your code.

Configure pack to use `heroku/buildpacks:20` as default Buildpack

```shell
pack config default-builder heroku/buildpacks:20
```

If everything goes well you should see *Builder heroku/buildpacks:20 is now the default builder*
in your CLI.

Build the image with pack build

```shell
pack build svx/fastapi-pip:1.0.0
```

Now you should see lots of CLI output, like pulling and extracting images and layers, this will take some minutes (depending on your internet connection and cache of local images).

When the build is successful you should see something like

*Successfully built image svx/fastapi-pip:1.0.0*

## Running

```shell
docker run -p 5000:5000 --name fastapi svx/fastapi-pip:1.0.0
```

Open your browser and browse to http://localhost:5000/