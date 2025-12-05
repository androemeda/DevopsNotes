Big picture:
- Pod → runs containers
- ReplicaSet → keeps pod count stable
- Deployment → manages ReplicaSets + upgrades

Everything builds on top of each other.

---

### Pods & Containers

Pod:
- smallest deployable unit
- represents one running instance
- can contain one or more containers
- containers inside pod share:
  - IP
  - network
  - volumes

Containers:
- lightweight
- fast startup
- package app + dependencies
- Kubernetes runs containers *inside pods*, not directly

---

### ReplicaSets (recap)

ReplicaSet:
- ensures fixed number of pods are always running
- maintains desired state

If something breaks:
- pod crashes → new pod created
- node dies → pod recreated on another node
- all automatic

ReplicaSet does **not** handle upgrades gracefully by itself.

---

### Deployments

Deployment:
- higher-level abstraction over ReplicaSet
- Deployment **creates and manages ReplicaSets**
- adds:
  - rolling updates
  - rollbacks
  - version history

Deployment controller:
- watches Deployment spec
- creates new ReplicaSet when version changes
- scales old ReplicaSet down and new one up

---

### Deployment YAML

Deployment YAML looks similar to ReplicaSet YAML.

Main difference:
- `kind: Deployment`

Important fields:
- replicas → number of pods
- template → pod definition
- labels → used to link Deployment → ReplicaSet → Pods

Example flow:
- change image version
- apply YAML
- Kubernetes creates a new ReplicaSet
- old ReplicaSet is gradually scaled down

---

### Scaling

Scaling options:
- `kubectl scale deployment <name> --replicas=N`
- update replicas in YAML

Deployment handles:
- increasing pod count
- decreasing pod count
- no manual pod management

---

### Rolling Updates

Default strategy:
- rolling update
- zero downtime

How it works:
- new pods come up first
- old pods are terminated gradually
- users never see full outage

Key point:
- traffic is always served by some pods

---

### Rollbacks

Deployment keeps revision history.

If upgrade fails:
- rollback to previous version
- old ReplicaSet becomes active again

Very useful in:
- CI/CD pipelines
- frequent releases

---

### Best Practices (from class)

- use declarative YAML, not imperative commands
- store YAMLs in version control
- avoid `kubectl run` / `kubectl edit` in production
- use namespaces for env separation (dev / test / prod)
- always monitor desired vs actual state

---

### Key Takeaways

- Pod runs containers
- ReplicaSet maintains pod count
- Deployment manages ReplicaSets
- Dep
