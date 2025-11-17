Containers recap:
- container ≠ VM, ≠ mini OS
- container = Linux process + namespaces + cgroups + temporary filesystem
- uses host kernel, not its own
- feels like a separate machine because of isolation

Why containers need volumes:
- containers are ephemeral by design
- when container stops → writable layer is deleted
- logs, temp files, DB data → gone
- volumes solve persistence problem

Docker volumes:
- Docker’s native way to persist data
- data lives outside container lifecycle
- container can be deleted, volume stays
- volumes can be shared across containers

Writable layer:
- every container has a writable layer on top of image
- image layers are read-only
- writable layer stores runtime changes
- deleted when container is removed

Types of storage:

Named volumes:
- created and managed by Docker
- reusable across containers
- stored under `/var/lib/docker/volumes/`
- preferred in production

Anonymous volumes:
- auto-created by Docker
- no user-defined name
- usually not reused
- harder to manage

Bind mounts:
- direct mapping to host filesystem path
- Docker does not manage location
- powerful but risky (permissions, path issues)
- common in local dev

Volume use cases:
- databases (MySQL, Postgres, Mongo)
- shared data between containers
- backups and logs
- separating data from application

Volume commands:
- create → `docker volume create vol_name`
- inspect → `docker volume inspect vol_name`
- attach → `docker run -v vol_name:/path image`
- read-only → `-v vol_name:/path:ro`

---

### Containers vs Virtual Machines (Deep)

Hypervisor (VM):
- each VM has:
  - its own OS
  - its own kernel
  - its own boot process
- heavy and slow to start
- boot flow:
  BIOS → MBR → Bootloader → Kernel → init → services

Containers:
- no BIOS, no bootloader, no kernel
- start main process directly
- startup time → milliseconds

---

### What Happens When You Run a Container

Command:
`docker run nginx`

Internal flow:
- docker client sends request
- containerd handles container creation
- runc uses Linux syscalls:
  - clone
  - unshare
  - chroot / pivot_root
- namespaces + cgroups created
- nginx starts as PID 1 inside container
- on host → just a normal process

Lifecycle:
- PID 1 exits → container stops
- writable layer removed
- namespaces destroyed
- cgroups released

Hence:
- container = process + temporary filesystem

---

### Namespaces (How Containers Get Their Own World)

Namespaces isolate:
- PID → container sees itself as PID 1
- NET → own IP, routing, ports
- MNT → own filesystem
- UTS → own hostname
- IPC → shared memory isolation
- USER → root inside container ≠ real root

---

### Why Containers Are Lightweight

- no OS boot
- no virtual hardware
- no kernel duplication
- only process isolation
- faster than even normal apps in many cases

---

### Ports & Networking

Port mapping:
`docker run -p host_port:container_port image`

Example:
- `-p 80:80`
- host port must be unique
- two containers cannot bind same host port
- internal container ports can be same

---

### Key Takeaways

- container is NOT a VM
- container is a Linux process
- isolation → namespaces
- limits → cgroups
- persistence → volumes / bind mounts
- Docker is fast because it skips OS boot
- containers are disposable by design
