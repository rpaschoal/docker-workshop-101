# Docker 101 Workshop

This repository contains the technical material for a Docker 101 Workshop.

## Workshop Agenda

* Pre-requisites
* Docker basic and useful commands
* Building your own image
* DockerHub and Private Repositories
* Running your container on the Cloud
* Docker Compose and container orchestration

## Pre-requisites

This workshop assume you have the following software installed on your machine:

* Docker Daemon or simply _Docker_
* .NET Core 2.2+ SDK
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
* A code editor such as Visual Studio, VS Code. Visual Studio is _not required_ but might be referenced or handy throughout this workshop

On top of the software listed above you'll also need an Azure account with a valid subscription to create a private Azure Container Registry.

To install Docker on Windows, please follow this link [Docker For Windows](https://docs.docker.com/docker-for-windows/)

_Note: Create a new resource group on azure for this workshop so it is easier to remove all the necessary resources once you've finished with them as they cost some $._

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

_Inspect the Dockerfile file on the root of your repository. See the build steps on this file. This is how we instruct the Docker daemon on how to build our custom images._

## DockerHub and Private Repositories

[Docker Hub](https://hub.docker.com/) is the official repository from Docker and it has support for public and private repositories. Most base images are retrieved from there and published by the companies maintaining it such as Microsoft, Node, etc.

For this workshop we'll be using a private container registry in Azure. Follow these instructions on how to create a Azure Container Registry instance: [Quickstart: Create a private container registry using the Azure portal](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-portal)

Once you have created it, lets push our locally built `aspnet` image to it by running the following CLI commands:

* `az acr login --name myregistry` _This command will sign in your local Docker daemon with your Azure Container Registry_
* `docker aspnetapp nginx myregistry.azurecr.io/aspnetapp` _This will tag your image with the container registry URL_
* `docker push myregistry.azurecr.io/aspnetapp` _This will push your image to the container registry_

And that's it, now if you go to your Azure portal and find your container registry instance you should see your image there! 🎉

## Running your container on the Cloud

https://docs.microsoft.com/en-us/azure/app-service/containers/tutorial-custom-docker-image

## Docker Compose and container orchestration

There is a docker-compose yaml file on this project that runs and build the `aspnet` image and starts up a SQL server container. They don't talk to each other on the application level for brevity of this workshop but they are network connected and enabled! Check it out by running `docker-compose up` on the root of your cloned repository! 🚀
