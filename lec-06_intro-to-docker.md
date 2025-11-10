Docker recap:
- Docker = platform to build, ship and run applications
- app + dependencies packed together as a container
- same container runs everywhere → no env issues

Containers:
- package code, libraries, configs together
- run reliably across systems
- lightweight because they share host OS kernel

Basic Docker commands:

docker run:
- creates a NEW container from image
- example: `docker run -it ubuntu bash`
- `-i` interactive, `-t` terminal

docker exec:
- used to enter an already running container
- example: `docker exec -it <container_id> bash`

Inspecting containers:
- `docker ps` → running containers
- `docker ps -a` → all containers
- `docker container inspect <id>` → detailed info (IP, config, network)

Docker images:
- containers always come from images
- images are read-only templates
- image = blueprint, container = running instance
- list images → `docker images`

Creating images:
- make changes inside a container
- save changes using `docker commit`
- `docker commit -m "msg" <container_id> <image_name>`

Docker Hub:
- default image registry
- to push image → name must start with dockerhub username
- `docker login`
- `docker push <username>/<image>`

Networking:
- containers get their own IP
- IP found using `docker inspect`
- containers can communicate using IP (curl, etc.)

Dockerfile & layers:
- images usually built using Dockerfile
- each instruction creates a new layer
- layers are cached → faster rebuilds
- commit = saving a new layer

Attached vs detached mode:
- foreground → `docker run nginx`
- background → `docker run -d nginx`

---

### Architecture Comparison

Bare metal:
- app runs directly on hardware
- no virtualization, no hypervisor
- full performance
- only one OS at a time

Hypervisor (Virtual Machines):
- hypervisor divides hardware into multiple VMs
- each VM has:
  - its own OS
  - its own kernel
  - its own boot process

Types:
- Type 1 → runs directly on hardware (ESXi, Hyper-V)
- Type 2 → runs on host OS (VirtualBox)

Why VMs are heavy:
- every VM boots full OS
- BIOS → MBR → Bootloader → Kernel → init → services
- repeated for each VM

Docker vs VM boot:
- Docker has NO BIOS, MBR, bootloader, kernel
- containers use host OS kernel
- container starts app directly
- startup time → milliseconds

Docker startup flow:
1. user runs `docker run <image>`
2. client sends request to daemon
3. daemon checks local image
4. pulls image if missing
5. creates container (fs, network, process isolation)
6. starts application instantly

Why Docker is lightweight:
- no OS boot
- single shared kernel
- only app + dependencies
- fast startup, small size

Docker architecture:
- Docker Client → CLI commands
- Docker Daemon → does all work
- Docker Host → runs daemon, stores images & containers
- Docker Registry → Docker Hub

Installing Docker:
- `curl -fsSL https://get.docker.com -o get-docker.sh`
- `sh get-docker.sh`
- verify using `docker run hello-world`

Important commands:
- `docker run`, `docker exec`
- `docker ps`, `docker ps -a`
- `docker start`
- `docker images`
- `docker commit`
- `docker push`
- `docker rmi`
