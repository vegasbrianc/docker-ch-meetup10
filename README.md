# Docker Swarm Demo
This demo will show how to deploy docker nodes using `docker-machine`, initialize theses nodes with Docker Swarm and deploy and scale an applicaiton to the Swarm.

# Agenda
- [Prerequisites](#prerequisites)
- [Deploy a standalone application to a single node](#deploy-a-standalone-application-to-a-single-node)
- Next
- next

## Prerequisites
Before we get started ensure you have [Docker for Mac](https://docs.docker.com/docker-for-mac/), [Docker for Windows](https://docs.docker.com/docker-for-windows/) or access to a Docker Host available running Docker version 1.12 or later.

## Deploy a standalone application to a single node
Before we can start Swarming let's revisit how current containers are deployed to a single node.

    docker run -d --name cats-app -p 5000:5000 markchurch/cats

