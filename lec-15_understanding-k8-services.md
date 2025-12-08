### Kubernetes (quick recap)
- open-source container orchestration platform
- automates deploy, scale and manage containerized apps
- works on a cluster of machines

---

### Pods

Pod:
- basic building block of Kubernetes
- represents a running process
- contains one or more containers

Pod characteristics:
- co-located → all containers run on same node
- co-started → containers start together
- shared networking → one IP per pod
- shared port space

Analogy:
- pod = house
- containers = rooms
- IP address belongs to the house, not the rooms

---

### ReplicaSets

ReplicaSet:
- ensures a fixed number of pods are always running
- maintains desired state

Key points:
- supports scale up / scale down
- if a pod crashes → new pod is created
- even for single pod apps, ReplicaSet is recommended
- gives fault tolerance for free

---

### Deployments

Deployment:
- higher-level object over ReplicaSet
- manages ReplicaSets and Pods

Features:
- declarative updates
- scaling made easy
- rolling updates (zero downtime)
- rollbacks to previous versions

Important:
- Deployment internally creates and manages ReplicaSets
- users usually interact with Deployments, not ReplicaSets directly

---

### Services

Why Services:
- pods are ephemeral
- pod IPs change when pods restart
- service gives a stable endpoint

Service:
- exposes a set of pods as a network service
- uses labels to find target pods
- provides load balancing

Types of Services:
- ClusterIP
  - default
  - accessible only inside cluster
- NodePort
  - exposes service on each node’s IP + fixed port
  - automatically creates a ClusterIP internally

Service discovery:
- services find pods using labels
- no hardcoding of pod IPs

Load balancing:
- traffic distributed evenly across pods

Analogy:
- multiple ticket counters
- you go to any counter, request is handled smoothly

---

### Load Balancers

Load balancer:
- distributes traffic across pods

Types:
- internal LB → within cluster
- external LB → exposes service to internet

Usually used with:
- cloud providers
- production traffic

---

### Kubernetes YAML Structure

Most YAML files contain:
- apiVersion → Kubernetes API version
- kind → object type (Pod, RS, Deployment, Service)
- metadata → name, labels, namespace
- spec → desired state

YA
