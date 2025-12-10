Big idea:
- Kubernetes networking decides **how things talk to each other**
- pods, services, nodes → all connected via cluster network
- networking is abstracted, but understanding flow is critical

---

### 1. Container ↔ Container (Same Pod)

Pod networking:
- pod is a **single network unit**
- all containers in a pod share:
  - same network namespace
  - same IP
  - same port space

Communication:
- containers talk using `localhost`
- no networking overhead
- behaves like multiple processes on same machine

Analogy:
- apps running on your laptop
- all using loopback interface (127.0.0.1)

---

### 2. Pod ↔ Pod (Same Node)

Same node communication:
- pods have different IPs
- communication happens via virtual network

How it works:
- CNI (Container Network Interface) plugin sets up networking
- creates virtual bridges, veth pairs
- packets routed internally on node

Network plugin:
- acts like a **bus driver**
- knows which pod lives where
- delivers traffic correctly inside the node

---

### 3. Pod ↔ Pod (Different Nodes)

Cross-node communication:
- more complex than same-node
- Kubernetes ensures **flat network**
- every pod can reach every other pod via IP

How it works:
- CNI plugin configures routing
- iptables rules added on nodes
- packets routed across node networks

kube-proxy:
- runs on every node
- maintains iptables rules
- helps route traffic to correct pod
- essential for service networking

---

### 4. Pod ↔ Service Communication

Why services exist:
- pods are ephemeral
- pod IPs change
- service provides stable endpoint

Service basics:
- service gets a ClusterIP
- service selects pods using labels
- traffic load-balanced across pods

Service discovery:
- handled by CoreDNS
- maps service name → ClusterIP
- pods talk using service name, not IP

Example:
- pod calls `http://my-service`
- CoreDNS resolves name
- kube-proxy routes traffic
- one of the matching pods receives request

Service internals:
- endpoints created for matching pods
- iptables rules forward traffic
- endpoints updated dynamically as pods change

---

### Important Commands

- `kubectl get svc`
- `kubectl describe svc`
- used to inspect service IPs, ports, selectors

---

### Namespaces & Labels

Namespaces:
- logical separation
- same service name can exist in differen
