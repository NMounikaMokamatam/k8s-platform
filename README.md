# k8s-platform

Kubernetes manifests and Helm charts for deploying microservices with full observability.

## Structure
## Features
- Zero-downtime rolling deployments
- Horizontal Pod Autoscaler (CPU + memory based)
- PodDisruptionBudget — minimum 2 pods always available
- Non-root container security context
- Prometheus scraping annotations built in
- Multi-zone topology spread constraints
- Liveness and readiness probes on every deployment

## Observability
Prometheus alert rules covering:
- Pod crash looping (critical)
- Pod not ready for 10+ minutes (warning)
- Node disk pressure (critical)
- Node CPU above 85% (warning)
- Service error rate above 5% (critical)
- p99 latency above 2s (warning)

## Deploy
```bash
# Deploy app with Helm
helm upgrade --install my-app ./helm/microservice/ \
  --namespace production \
  --set appName=my-app \
  --set image.tag=v1.2.3 \
  --set environment=production \
  --wait --timeout 5m

# Apply Prometheus alert rules
kubectl apply -f observability/prometheus/alerts.yaml -n monitoring
```
