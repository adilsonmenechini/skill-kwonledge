---
type: guide
category: kubernetes
tags: [ingress, routing, http, load-balancing]
status: active
created: 2026-04-27
---

# Kubernetes Ingress

## Overview
Ingress is an API object that manages external HTTP/HTTPS access to services, providing URL routing, SSL termination, and load balancing.

## Purpose
Ingress exposes services to the outside world:
- Single entry point for multiple services
- Path-based or host-based routing
- SSL/TLS termination
- Custom load balancing

## Content

### Ingress Resource

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: example.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
      - path: /web
        pathType: Prefix
        backend:
          service:
            name: web-service
            port:
              number: 80
```

### TLS Termination

```yaml
spec:
  tls:
  - hosts:
    - example.com
    secretName: tls-secret
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: web-service
            port:
              number: 80
```

## Usage

### Common Annotations

```yaml
annotations:
  # Rewrite paths
  nginx.ingress.kubernetes.io/rewrite-target: /api/$2
  
  # Custom max body size
  nginx.ingress.kubernetes.io/proxy-body-size: "10m"
  
  # Rate limiting
  nginx.ingress.kubernetes.io/limit-connections: "10"
  nginx.ingress.kubernetes.io/limit-rps: "5"
  
  # Redirect HTTP to HTTPS
  nginx.ingress.kubernetes.io/ssl-redirect: "true"
```

### Commands

```bash
# Create ingress
kubectl apply -f ingress.yaml

# List ingresses
kubectl get ingress

# Describe ingress
kubectl describe ingress my-ingress

# Check ingress controller
kubectl get pods -n ingress-nginx
```

### Ingress Controllers

| Controller | Provider |
|-----------|----------|
| nginx-ingress | Community |
| ingress-nginx | Kubernetes |
| AWS ALB | AWS |
| GCE | Google Cloud |
| Traefik | Containous |

## Relationships
- [[kubernetes-services]]
- [[kubernetes-architecture]]

## Notes
- Requires Ingress Controller deployment
- Path handling varies by controller
- Use annotations for controller-specific settings

## References
- [Ingress Documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [ingress-nginx](https://kubernetes.github.io/ingress-nginx/)