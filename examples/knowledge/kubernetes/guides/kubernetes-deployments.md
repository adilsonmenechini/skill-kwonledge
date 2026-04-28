---
type: guide
category: kubernetes
tags: [deployment, yaml, configuration, rolling-update]
status: active
created: 2026-04-27
---

# Kubernetes Deployments

## Overview
A Deployment provides declarative updates for Pods and ReplicaSets. It describes the desired state for your application and Kubernetes automatically manages the actual state.

## Purpose
Deployments are used to:
- Create new versions of applications (rolling updates)
- Roll back to previous versions
- Scale applications up or down
- Pause and resume deployments
- Ensure high availability through replica management

## Content

### Deployment Specification

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:v1.0.0
        ports:
        - containerPort: 8080
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
```

### Key Fields

| Field | Description |
|-------|-------------|
| `replicas` | Number of identical Pods to run |
| `selector` | How Deployment finds Pods to manage |
| `strategy` | Update strategy (RollingUpdate or Recreate) |
| `maxSurge` | Extra pods allowed during update |
| `maxUnavailable` | Pods that can be unavailable during update |

## Usage

### Common Operations

```bash
# Create deployment
kubectl apply -f deployment.yaml

# Check deployment status
kubectl rollout status deployment/my-app

# View deployment details
kubectl describe deployment my-app

# Scale deployment
kubectl scale deployment/my-app --replicas=5

# Update image version
kubectl set image deployment/my-app my-app=my-app:v2.0.0

# Rollback to previous version
kubectl rollout undo deployment/my-app

# View rollout history
kubectl rollout history deployment/my-app
```

### Deployment Strategies

1. **RollingUpdate** (default): Gradually replaces old pods with new ones
2. **Recreate**: Terminates all pods before creating new ones (causes downtime)

## Relationships
- [[kubernetes-architecture]]
- [[kubernetes-pods]]
- [[kubernetes-services]]

## Notes
- Always set resource limits to prevent resource starvation
- Use readiness probes to ensure traffic only goes to ready pods
- Liveness probes detect when containers need restart

## References
- [Deployments Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Rolling Updates](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)