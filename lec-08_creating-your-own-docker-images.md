## lec 8 – Containers Internals & How Docker Works

Containers:
- way to package app + dependencies together
- create isolated environments on same OS
- same setup for dev, test and prod

History:
- idea of isolation is old
- `chroot` in Unix (1960s–70s)
- creates filesystem “jail” for a process
- still shares same kernel → not full isolation

What is a container:
- lightweight executable package
- contains code, runtime, libs, system tools
- does NOT ship its own OS
- shares host OS kernel

Containers vs VMs:
- containers are lightweight
- VMs bundle full OS + kernel
- container startup is fast
- VM startup is slow due to boot process

Isolation:
- both VMs and containers isolate workloads
- VMs use hypervisor
- containers use Linux kernel features

How containers work internally:

Namespaces:
- provide isolation
- isolate:
  - process IDs
  - hostname
  - network
  - users
  - IPC
  - filesystem

Cgroups (control groups):
- control resource usage
- limit CPU, memory, etc.
- prevent one container from hogging resources

Docker & kernel:
- Docker talks directly to Linux kernel
- no hypervisor on Linux
- uses kernel features for isolation and control

Docker on different OS:
- Linux → containers run natively
- Windows / macOS → Docker runs inside a lightweight Linux VM
- reason: Docker needs Linux kernel features

Ephemeral nature of containers:
- containers are disposable
- can be stopped, deleted, recreated anytime
- no guarantee of data persistence
- apps should be stateless
- data should live outside (volumes, DBs)

Networking & ports:
- containers have isolated network stack
- not directly accessible from host
- port mapping used to expose services
- example: host_port → container_port

Why containers are powerful:
- fast startup
- efficient resource usage
- easy scaling
- consistent environments everywhere

Key takeaway:
- containers = kernel-level isolation, not OS-level
- Docker is thin layer over Linux kernel
- understanding namespaces + cgroups is core to Docker
