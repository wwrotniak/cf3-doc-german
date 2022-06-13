How to use Docker
=================

Installation in Ubuntu:

::

   sudo apt update

   sudo apt install apt-transport-https ca-certificates gnupg-agent software-properties-common

   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

   sudo apt install docker-ce docker-ce-cli containerd.io
   
 
Installation in CentOS:
 
::
 
   sudo yum install -y yum-utils
   
   sudo yum-config-manager \
       --add-repo \
       https://download.docker.com/linux/centos/docker-ce.repo
   
   sudo yum install docker-ce docker-ce-cli containerd.io

   sudo systemctl start docker
   

Verify Docker installation by running the ``hello-world`` image:


::

   sudo docker run hello-world
   
   
You should get output similar to this:

::

   Unable to find image 'hello-world:latest' locally
   latest: Pulling from library/hello-world
   0e03bdcc26d7: Pull complete
   Digest: sha256:e7c70bb24b462baa86c102610182e3efcb12a04854e8c582838d92970a09f323
   Status: Downloaded newer image for hello-world:latest
   
   Hello from Docker!
   This message shows that your installation appears to be working correctly.
   
   To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
       (amd64)
    3. The Docker daemon created a new container from that image which runs the
       executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
       to your terminal.
   
   To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash
   
   Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/
   
   For more examples and ideas, visit:
    https://docs.docker.com/get-started/
    


To download docker images (in this case ubuntu) we need to use:

::

   sudo docker pull ubuntu
   
   
For more pre-configured images check: `hub.docker.com <https://hub.docker.com>`_


if you want to see what images you have already downloaded use:

::

   sudo docker images
      
   REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
   ubuntu        latest    ba6acccedd29   5 weeks ago    72.8MB
   hello-world   latest    feb5d9fea6a5   2 months ago   13.3kB
   
   
To create and run docker container:

**docker run**

eg.:

::

   docker run ubuntu -it

 

Of course you can create a container and run it later, to do this:

::

   docker create

And when you want to start using the container:

::

   docker start <id>

To enter running container with interactive mode and tty use:

::

   docker exec -it <id> /bin/bash

 

To stop/start/remove docker image:

::

   docker stop/start/rm <id>

To list working docker images:

::
   
   docker ps -a
