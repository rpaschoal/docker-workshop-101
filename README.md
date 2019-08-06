# Docker 101 Workshop

This repository contains the technical material for a Docker 101 Workshop.

## Workshop Agenda

* Pre-requisites
* Docker basic and useful commands
* Building your own image
* DockerHub and Private Repositories
* Docker Compose and container orchestration

## Pre-requisites

This workshop assume you have the following software installed on your machine:

* Docker Daemon or simply _Docker_
* .NET Core 2.2+ SDK
* A code editor such as Visual Studio, VS Code. Visual Studio is _not required_ but might be referenced or handy throughout this workshop

On top of the software listed above you'll also need an Azure account with a valid subscription to create a private Azure Container Registry.

To install Docker on Windows, please follow this link [Docker For Windows](https://docs.docker.com/docker-for-windows/)

## Docker basic and useful commands

Before we move on to creating our container image it is important that every reader that is following through this workshop to understand the basic commands and concepts behind Docker. I've written an article in the past that should be a good starting point to understand the reasonings, foundations and basic/curated list of commands for Docker. Please take a time to read it: [How to get started with Docker on Windows](https://www.scalablepath.com/blog/get-started-docker-windows/)

Windows is planning on shipping a Linux dist with Windows 10 which should make things smoother and better for those running Docker on Windows ❤️

## Building your own image

Within the root directory where you cloned this repository, run the following set of commands:

```
cd aspnetapp
docker build --pull -t aspnetapp .
docker run --name aspnetcore_sample --rm -it -p 8000:80 aspnetapp
```

You should see the following console output as the application starts:

```
C:\git\dotnet-docker\samples\aspnetapp>docker run --name aspnetcore_sample --rm -it -p 8000:80 aspnetapp
Hosting environment: Production
Content root path: /app
Now listening on: http://[::]:80
Application started. Press Ctrl+C to shut down.
```

After the application starts, navigate to http://localhost:8000 in your web browser. You should now see the ASPNET sample application response.

