### What is HPA

HPA (Horizontal Pod Autoscaler):
- Kubernetes resource for **automatic scaling**
- changes number of pod replicas
- works with:
  - Deployment
  - ReplicaSet
  - StatefulSet

Scaling is based on:
- CPU utilization (most common)
- memory
- custom / external metrics

Idea:
- load ↑ → pods ↑
- load ↓ → pods ↓
- no manual intervention

Analogy used:
- if workload increases, you hire more people
- HPA does the same by adding more pods
- this is **horizontal scaling** (more pods, not bigger pods)

---

### Prerequisites for HPA

Kubernetes cluster:
- usually set up using `kubeadm`

Required components:
- kubeadm → cluster setup
- kubectl → interact with cluster
- kubelet → runs on each node

Metrics Server (VERY IMPORTANT):
- collects CPU & memory metrics
- exposes metrics via Kubernetes API
- HPA **will not work without metrics server**

If metrics server is missing:
- `kubectl top` fails
- HPA cannot scale
- common beginner mistake

---

### Important Commands Discussed

Apply YAML:
- `kubectl apply -f file.yaml`

Manual scaling (for comparison):
- `kubectl scale --replicas=5 deployment/myapp`

Check resource usage:
- `kubectl top pods`
- `kubectl top nodes`
- requires metrics server

Monitoring:
- `kubectl get pods`
- `kubectl get hpa`

---

### Deploying HPA (High-level Flow)

1. Create a Deployment
- app must already be running
- replicas initially set manually

2. Deploy Metrics Server
- enables CPU / memory tracking

3. Create HPA resource
- define:
  - min replicas
  - max replicas
  - target CPU utilization (e.g. 50%)

Example logic:
- CPU > 50% → scale up
- CPU < threshold → scale down
- replicas stay within min–max range

---

### How HPA Works Internally

- metrics server reports CPU usage
- HPA controller compares:
  - current usage vs target usage
- if threshold crossed:
  - HPA updates replica count
- Deployment contr
