# Docker Basics

***
**The following is simply an amalgamation of information from various sources that I believed to be useful. I am compiling all of these details into one document to not only make important information easier for me to look back on, but also potentially help future Docker learners.**
***

## What is Docker?

* A software platform that simplifies the process of developing, running, and distributing applications using [containers](#What+are+containers?), which are based on [images](#What+are+images?).
* Key advantages:
     * Unlike virtual machines, which require those on the external end to tediously install the host's operating system in order to be able to do anything with an application, Docker containers are **process-isolated** and **share** the host's OS.
          * This makes Docker containers super speedy (can take only a few seconds to boot), as they are much smaller and use far less resources than a VM (which can take at least a couple minutes to boot).

## What are images?

* A packaged set of instructions that specifies what will be run inside of some container
* Often not built from scratch - old images can be modified to become applicable to a given project 
* Typically describe...
     * Which existing image will be used as a foundation for our container
     * Specific commands to be run for future containers
     * What the file system will look like in the container
     * Other operating instructions, such as which ports would be needed to open the container and how to import data from a specified host system
* The information above is usually written in a Dockerfile
     * Docker generates a container image based on the Dockerfile through the `docker build` command

## What are containers?

* A way to execute images (the "packaged set of instructions") in a runtime environment
* Multiple containers can be created from a single image
     * This can be useful when testing different versions of some base program, for example. All versions can be tested simultaneously in their own containers, which saves a lot of time compared to if you were to run each version of the program one after the other 
* Containers can never update an image, which is read-only outside of its associated Dockerfile
* Running a container:
     * The `docker run` command is used to start a container
     * Containers will run indefinitely until they either fail or are told to stop
          * While running, they cannot update themselves if any changes are made to the image on which they are based. You must stop, remove, and restart all containers based on this image in order to successfully update them

## A helpful analogy

Consider this very useful analogy by DevOps analyst Chris Tozzi from his explanation of containers vs. images:

* Think of a Docker image as the recipe for a cake, and a container as the cake you have baked from said recipe.
* The image tells you exactly what ingredients are required for the cake. You will obviously have no finished product that you can eat if you simply stop here after reading the instructions.
* The container is the cake. You must follow the instructions from the recipe if you want to create an end product that can be eaten. Similarly, we need to follow the instructions given by the image in order to be able to start a container that has a certain function/purpose (more specifically, a container that can execute some software/service that it runs).
* Any number of cakes can be made from a single recipe. If you've already made some number of cakes but then decide to change the recipe, this will not change any of the cakes that you have previously made. Only the new cakes you make going forward can be made using the updated recipe. In the same way, containers that are currently running cannot be changed if their associated image is updated midway. Only new containers made from the updated image will display this change.

## Additional terminology

* **Docker Hub** - a registry/directory of all available Docker images that you can use as your "base program" for your containers. You can also host your own registry for pulling images if needed.
* **Docker Daemon** - the service that runs behind-the-scenes to manage the building, running, and distributing of Docker containers. It runs in the OS which clients can communicate with.
* **Docker Client** - the command line tool that enables users to interact with the daemon. For example, Kinematic is a client that provides users with a GUI.


***
## Sources
* [Docker overview](https://docs.docker.com/get-started/overview/)
* [Docker for beginners](https://docker-curriculum.com/)
* [What is a Docker container vs. an image?](https://www.techtarget.com/searchitoperations/answer/What-is-a-Docker-container-vs-an-image)
* [Manage repositories](https://docs.docker.com/docker-hub/repos/)
***
