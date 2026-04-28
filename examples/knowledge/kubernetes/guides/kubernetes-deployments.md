---
title: Kubernetes Deployments
type: guide
category: kubernetes
tags:
  - deployment
  - yaml
  - configuration
  - rolling-update
aliases:
  - k8s deployment
  - deployment-guide
status: active
created: 2026-04-27
updated: 2026-04-27
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
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:latest
        ports:
        - containerPort: 8080
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
          requests:
            memory: "64Mi"
            cpu: "250m"
```

### Rolling Update Strategy

```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
```

### Commands

```bash
# Create deployment
kubectl apply -f deployment.yaml

# List deployments
kubectl get deployments

# Scale deployment
kubectl scale deployment my-app --replicas=5

# Update image
kubectl set image deployment/my-app my-app=new-version

# Check rollout status
kubectl rollout status deployment/my-app

# Rollback to previous
kubectl rollout undo deployment/my-app

# Rollback to specific revision
kubectl rollout undo deployment/my-app --to-revision=2

# View rollout history
kubectl rollout history deployment/my-app

# Pause deployment
kubectl rollout pause deployment/my-app

# Resume deployment
kubectl rollout resume deployment/my-app
```

## Usage Examples

### Create from CLI

```bash
# Create deployment from image
kubectl create deployment my-app --image=nginx --replicas=3

# Expose deployment as service
kubectl expose deployment my-app --port=80 --type=LoadBalancer
```

### Scaling

```bash
# Scale to specific count
kubectl scale deployment my-app --replicas=10

# Scale based on CPU usage
kubectl autoscale deployment my-app --min=2 --max=10 --cpu-percent=80
```

## Relationships
- [[kubernetes-architecture]]
- [[kubernetes-pods]]
- [[kubernetes-services]]

## Notes
> [!tip]
> Always set resource requests and limits for production workloads

- Use readiness probes for production
- Set appropriate `maxUnavailable` for zero-downtime updates

## References
- [Deployments Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Rolling Updates](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment)
