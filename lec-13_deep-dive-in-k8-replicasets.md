### Kubernetes YAML basics

Most Kubernetes YAML files have 4 main parts:
- apiVersion → API version being used
- kind → type of object (Pod, ReplicaSet, Deployment, etc.)
- metadata → info about object (name, labels, etc.)
- spec → what you want Kubernetes to create (varies by object)

YAML data types:
- key-value → `key: value`
- list → `- item`
- map → nested key-value structures

---

### Pods

Pod:
- smallest deployable unit in Kubernetes
- contains one or more containers
- containers inside pod:
  - share same IP
  - share network namespace
  - share volumes
- co-located and co-scheduled on same node

Crash handling:
- if a container crashes, Kubernetes recreates it automatically
- analogy used: hero keeps getting replaced in a movie
- user does not manually restart containers

---

### ReplicaSets

Why ReplicaSets:
- ensures a fixed number of pod replicas are always running
- maintains desired state

Example:
- replicas: 100
- if one pod dies → ReplicaSet creates a new one
- if node goes down → pods are recreated on other nodes

ReplicaSet YAML structure:
- kind: ReplicaSet
- replicas: desired pod count
- selector:
  - matches labels of pods it should manage
- template:
  - pod definition
  - labels must match selector

Labels:
- used to group and identify pods
- similar to tags in cloud platforms (AWS)

---

### Internal Working

API Server:
- entry point to cluster
- handles authentication, authorization, validation
- stores state in etcd

etcd:
- key-value store
- holds cluster state

Scheduler:
- decides which node pod should run on
- based on CPU, RAM, constraints

Controller (ReplicaSet controller):
- continuously compares:
  - desired state vs actual state
- takes corrective action if mismatch

Kubelet:
- runs on each node
- creates, runs, and monitors pods
- reports node and pod status to API server

---

### Pod lifecycle & recovery

- controller watches pod count
- if pod fails:
  - controller notifies API server
  - new pod is scheduled
- self-healing is automatic

---

### Common kubectl commands

- create / update → `kubectl apply -f file.yaml`
- delete → `kubectl delete -f file.yaml`
- list resources → `kubectl get pods`
- list replicasets → `kubectl get rs`

---

### Key Takeaways

- YAML structure is consistent across objects
- pod is the execution unit
- ReplicaSet maintains pod count
- labels + selectors are critical
- Kubernetes constantly enforces desired state
