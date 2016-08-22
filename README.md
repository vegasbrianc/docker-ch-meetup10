# Docker Swarm Demo
This demo will show how to deploy docker nodes using `docker-machine`, initialize theses nodes with Docker Swarm and deploy and scale an applicaiton to the Swarm.

# Agenda
- [Prerequisites](#prerequisites)
- [Deploy a standalone application to a single node](#deploy-app)
- [Build the Swarm](#Step-2-Build-Swarm)
- next

## Prerequisites
Before we get started ensure you have [Docker for Mac](https://docs.docker.com/docker-for-mac/), [Docker for Windows](https://docs.docker.com/docker-for-windows/) or access to a Docker Host available running Docker version 1.12 or later.

## <a name="deploy-app"></a>Step 1. Deploy a standalone application to a single node
Before we can start Swarming let's revisit how current containers are deployed to a single node.

    docker run -d --name cats-app -p 5000:5000 markchurch/cats

Verify the container is running
    
    `docker ps`

Test the container

    `curl 0.0.0.0:5000`

![Curl Demo](https://github.com/vegasbrianc/docker-ch-meetup10/images/curl_demo.png)

## <a name="Build-Swarm"></a>Step 2. Build the Swarm
"If you build it, the containers will come."

Deploying a container to a single host is awesome and has a ton of use cases. However, a single host doens't offer higher performance and availability that is required for some productions applications. This is where Docker Swarm comes in.

A Docker Swarm is a group of Docker Engines that are combined into a self-orchestrating group called a Swarm. Swarm mode contains the feature services that allows us to deploy and manage multi-container applicationss across our Docker Swarm which can contain multiple or more Docker hosts.

We will create 4 new Docker Hosts. 1 x Docker Swarm Manager and 3 x Docker Nodes. The Swarm Manager is responsible to maintain/monitors the state of the swarm and schedules containers across the Swarm. The Docker Nodes run the workload of the Swarm.

### Step 2.1 Build and Deploy a Swarm Manager
