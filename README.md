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

    docker ps

Test the container

    curl 0.0.0.0:5000

Now you should see a cat of the day:
![Curl Demo](https://github.com/vegasbrianc/docker-ch-meetup10/blob/master/images/curl_demo.png)

## <a name="Build-Swarm"></a>Step 2. Build the Swarm
"If you build it, the containers will come."

Deploying a container to a single host is awesome and has a ton of use cases. However, a single host doens't offer higher performance and availability that is required for some productions applications. This is where Docker Swarm comes in.

A Docker Swarm is a group of Docker Engines that are combined into a self-orchestrating group called a Swarm. Swarm mode contains the feature services that allows us to deploy and manage multi-container applicationss across our Docker Swarm which can contain multiple or more Docker hosts.

We will create 4 new Docker Hosts. 1 x Docker Swarm Manager and 2 x Docker Nodes. The Swarm Manager is responsible to maintain/monitors the state of the swarm and schedules containers across the Swarm. The Docker Nodes run the workload of the Swarm.

### Step 2.1 Build and Deploy a Swarm Manager
Time to setup our first node in our Swarm. The first node will be the Swarm Manager.

    docker-machine create -d virtualbox mgr

This will create a virtual machine with the name of mgr. Once the command completes let's check the status of our newly created machine.

    docker-machine ls
    NAME   ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER    ERRORS
    mgr    *        virtualbox   Running   tcp://192.168.99.100:2376           v1.12.1

Record the IP address of our Swarm Manager as we will use it to initalize the Swarm. Let's connect to our newly created Swarm Manager

    docker-machine ssh mgr

Once connected let's initialize our Swarm

    docker swarm init --advertise-addr 192.168.99.100

Upond command completion you will notice two commands printed. Record the command for adding a work node for later. For visualization purposes we will run a Swarm Visualizer created by [Swarm Visulaizer](https://github.com/ManoMarks/docker-swarm-visualizer)

    docker run -it -d -p 8080:8080 -e HOST=192.168.99.100 -v /var/run/docker.sock:/var/run/docker.sock manomarks/visualizer
    
Open the visualizer to monitor changes to your swarm at `http://192.168.99.100:8080`

![Swarm Visualizer](https://github.com/vegasbrianc/docker-ch-meetup10/blob/master/images/swarm_mgr.png)


### Step 2.2 Create Docker Swarm Nodes
Now our manager is up and running and ready to accept worker connections. We will add new nodes to our Swarm and watch our visualizer as they come online. Go ahead and create node01 and node02.

    docker-machine create -d virtualbox node01
    docker-machine create -d virtualbox node02
    
Once the nodes have successfuly been created we will join them to the swarm. First, we need the Swarm Token in order to make this happen.

    docker swarm join-token worker
    To add a worker to this swarm, run the following command:
     docker swarm join \
    --token SWMTKN-1-1vh7h94m797al5a4pcma4p7nxdw22vqa2udwgkrkcd0twsz92d-4xgkpsqo1wyi0v7m4pnqcv2eq \
    192.168.99.100:237

Copy the command as we will run this on the newly created nodes.

    docker-machine ssh node01

Paste the `docker swarm join` command from above into node01. Node01 should now be part of the Swarm. SSH into node02 and complete the same step. 

Now our Swarm is complete. We have 1 Swarm Manager and 2 worker nodes.
![Swarm Visualizer](https://github.com/vegasbrianc/docker-ch-meetup10/blob/master/images/swarm_all_nodes.png)

