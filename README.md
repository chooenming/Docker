# What is Docker?
* Virtualisation software makes developing and deploying applications much easier
* Package application with all necessary dependencies, configuration, system tools, and runtime (aka container)
* Application and its running environment are packaged in a single Docker package (easily share and distributed)

# Importances of Docker
* Start service as a Docker container using a 1 Docker command
* Command the same for all OS
* Command same for all services
* Standardizes process of running any service on any local dev environment
* Easy to run different versions of same app without any conflicts
* No configurations needed on the server (except Docker runtime)

# How an OS is Made Up?
* 2 layers:
    * OS Application Layer:
        * Run on top of kernel
    * OS Kernel:
        * Core of every OS
        * Part that communicates with hardware and software components (CPU, memory, storage)

# Virtual Machine vs Docker
| Virtual Machine | Docker |
| ---------- | ---------- |
| Virtualize the complete OS (Application Layer and Kernel)  | Virtualize the application layers |
| Use its own kernel  | Use the kernel of the host |
| Image larger (couple of GB) | Docker images smaller (couple of MB) |
| Take minutes to start | Take seconds to start |
| Compatible with all OS (Linux based Docker images, cannot use Window kernel) | Compatible only with Linux distros |
| | Use hypervisor layer with a lightweight Linux distro (provide the needs of Linux kernel) to make running the containers possible on Window and MacOS |

# Docker Image vs Docker Containers
| Docker Image | Docker Containers |
| ---------- | ---------- |
| An executable application artifact (Immutable template that defines how a container will be realized) | A running instance of an image |
| Includes app source code, but also complete environment configuration | That is when the container environment is created |
| Add environment variables, create directories, files etc | Can run multiple containers from 1 image |

# Docker Registries
* A storage and distribution system for Docker images
* Docker hosts one of the biggest Docker Registry, called "Docker Hub"
* Docker tags are used to identify images by name (version controlling)
## Private Registries
* Need to authenticate before accessing the registry

# Registry vs Repository
* Docker Registry
    * A service providing storage
    * Can be hosted by a third party, like AWS, or by yourself
    * Collection of repositories
* Docker Repository
    * Collection of related images with same name but different version

# Container Port vs Host Port
* Application inside container runs in an isolated Docker network, which allows to run the same app running on the same port multiple times
* Need to expose the container port to the host (the machine the container runs on) ->> Port Binding
* Can view the port using command: docker ps
* Port Binding: after binding, can access the container as if it is running on local host port (search localhost:<host port> on the browser)
* Only 1 service can run on a specific port on the host
## Choosing Host Port
* Standard to use the same port on host as container is using
* If container uses 8000, then bind to local host on 8000

# Building Own Docker Image
## Dockerfile
* Text document that contains commands to assemble an image
* Docker can then build an image by reading those instructions
* Each instruction in the Dockerfile creates one layer (Docker image consists of many layers)
* These layers are stacked and each one is a delta of the changes from the previous layer
### Structure of Dockerfile
* Start from a parent image or "base image"
* It's a Docker image that your image is based on
* Choose the base image, depending on which tools you need to have available
* FROM
    * Must begin with a FROM instruction (build this image FROM specific image)
* RUN
    * Execute any command in a shell inside the container environment
* COPY
    * Copies files or directories from <src> and adds them to the filesystem of the container at the path <dest>
    * While "RUN" is executed in the container, "COPY" is executed on the host
* WORKDIR
    * Sets the working directory for all following commands
    * Like changing into a directory: "cd ..."
* CMD
    * The instruction that is to be executes when a Docker container starts
    * There can only be on "CMD" instruction in a Docker file
#### Multi-Layer Approach
* Every image consists of multiple iamge layers
* This makes Docker so efficient, because image layers can be cached

# Special Notes
* Docker pull images automatically if it is not found on local