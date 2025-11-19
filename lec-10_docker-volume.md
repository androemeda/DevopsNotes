### Docker Networking Basics

Why networking matters:
- containers need to talk to:
  - other containers
  - host machine
  - external world
- Docker handles networking automatically but concepts matter

IP addresses:
- every container gets its own IP
- IP used for container-to-container communication
- managed by Docker internally

Subnetting:
- network divided into smaller networks
- CIDR notation used
- example: `192.168.10.0/24`
  - /24 → 8 host bits
  - total IPs = 2⁸ = 256

Network ID & Broadcast ID:
- first IP → network ID (identifies network)
- last IP → broadcast ID (talk to all devices)
- neither can be assigned to a container

Docker zero bridge (docker0):
- created automatically when Docker is installed
- acts like a virtual switch
- every container has:
  - `eth0` inside container
  - connected to docker0 using veth pair
- allows container ↔ container ↔ internet communication

Default bridge network:
- containers launched without custom network attach to docker0
- containers can communicate using IPs
- custom bridge networks can be created if needed

Custom bridge network:
- `docker network create my_bridge`
- supports custom subnets and gateways
- containers in same bridge can talk directly

Inspect networking:
- `docker inspect <container_id>`
- shows IP, gateway, network details

Subnetting example (logical separation):
- engineering → `192.168.10.0/26`
- HR → `192.168.10.64/26`
- reception → `192.168.10.128/26`
- each subnet is isolated

---

### Why Docker Needs Volumes

Containers are ephemeral:
- image layers → read-only
- container adds writable layer
- writable layer deleted when container is removed

Important clarification:
- stop + start → data stays
- remove container → data lost

Writable layer:
- stores runtime file changes
- temporary by design
- not meant for persistent data

---

### Docker Volumes

What is a volume:
- storage managed by Docker
- lives outside container lifecycle
- stored under `/var/lib/docker/volumes`
- survives container deletion

Why volumes:
- databases need persistence
- containers are disposable
- volumes decouple data from app

---

### Types of Docker Storage

Anonymous volumes:
- auto-created
- random name
- tied to container lifecycle
- temporary usage

Named volumes:
- explicitly created
- reusable
- best for production
- commonly used for DBs

Commands:
- create → `docker volume create vol_name`
- inspect → `docker volume inspect vol_name`
- use → `-v vol_name:/path`

Bind mounts:
- map host path directly
- `-v /host/path:/container/path`
- instant reflection of changes
- useful in dev
- risky in production

tmpfs mounts:
- stored in RAM only
- data never written to disk
- wiped on container stop
- used for cache, secrets

---

### Volume Persistence Example

Stop/start:
- data remains because container exists

Remove container:
- writable layer deleted

Volume-backed data:
- persists even after container removal
- multiple containers can mount same volume
- enables real-time file sharing

---

### Port Mapping Rule

Syntax:
`-p host_port:container_port`

Rules:
- host port must be unique
- two containers cannot bind same host port
- container ports can be same internally

---

### Key Takeaways

- container = process, not OS
- networking handled via bridges + namespaces
- docker0 acts like virtual switch
- data is lost only when container is removed
- volumes persist data beyond container lifecycle
- named volumes → production
- bind mounts → development
- tmpfs → sensitive / temporary data
