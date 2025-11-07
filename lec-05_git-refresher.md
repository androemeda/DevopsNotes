Docker:
- platform to create and run containers
- packages app + dependencies together
- idea → “if it fits, it ships”  
  once app runs in a container, it can run anywhere Docker is available

Core concepts:

Images:
- read-only templates / blueprints
- contain app + dependencies
- containers are always created from images
- analogy → image = class, container = object

Containers:
- lightweight, isolated runtime environments
- have their own filesystem and processes
- share host OS kernel (unlike VMs)
- faster and lighter than virtual machines

Docker architecture:

Docker client:
- CLI tool (`docker`)
- user interacts with this
- sends commands to daemon

Docker daemon:
- background service
- pulls images
- creates and runs containers
- manages container lifecycle

Daemon = background service in Linux  
check using `systemctl status docker`

Running containers:
- `docker run <image>`
- always creates a NEW container
- if image not found locally → pulled from Docker Hub

Example:
- `docker run hello-world`
- shows how client talks to daemon
- daemon pulls image, creates container, runs it

Docker Hub:
- default public image repository
- images can be local or remote

Getting inside a container:
- `docker run -it ubuntu bash`
- `-i` → interactive
- `-t` → terminal
- `bash` → shell inside container
- hostname changes to container ID

Processes in containers:
- containers have isolated process space
- `ps -ef` inside container shows only container processes

Volumes:
- used for persistent data
- data should not live inside container filesystem

Networking:
- Docker provides its own networking
- containers can talk to each other and external systems

Docker on AWS EC2:
- SSH into EC2 using `.pem` key
- install Docker on instance
- Docker usage same as local machine

Important takeaways:
- images are immutable artifacts
- containers are disposable
- docker run = pull (if needed) + create + start
- Docker = foundation for learning Kubernetes
