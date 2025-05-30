# Summary

[Crafteo - Kubernetes Training](welcome.md)

# Introduction

- [Our first Pod](intro/pod.md)
- [Deployment](intro/deployment.md)
- [Service](intro/service.md)
- [Logs, exec and other operations](intro/logs-exec-others.md)

# Controllers 

- [Deployments & ReplicaSets](controllers/deployments.md)
- [Jobs & CronJobs](controllers/jobs.md)
- [DaemonSets](controllers/daemonsets.md)
- [StatefulSets](controllers/statefulsets.md)

# Services & Networking

- [NodePort](services/nodeport.md)
- [LoadBalancer](services/loadbalancers.md)
- [Ingresses and Ingress Controllers](services/ingresses.md)
- [ExternalName Services](services/externalname.md)
- [Advanced: Endpoints, Headless Service, Service discovery...](services/advanced.md)

# Configs & Secrets

- [ConfigMap](config/configmap.md)
- [Secret](config/secret.md)

# Volumes: Persistent & Ephemeral

- [Persistent Volumes: PVC & PV](volumes/pvc.md)
- [Ephemeral Volumes: emptyDir](volumes/emptydir.md)

# Deployment tools

- [Helm: introduction](deploy-tools/helm-intro.md)
- [Helm: advanced](deploy-tools/helm-advanced.md)
- [Kustomize](deploy-tools/kustomize.md)

# Deploy in Production

- [Ingress & TLS / HTTPS](production/tls.md)
- [Resources Requests & Limits](production/resources.md)
- [Horizontal Scalability](production/horizontal-scaling.md)
- [Vertical Scalability](production/vertical-scaling.md)
- [Liveness, Readiness and Startup Probes](production/probes.md)
- [Pod Disruption Budget (PDB)](production/pdb.md)

# Scheduling

- [Introduction](scheduling/intro.md)
- [Topology Spread Constraint](scheduling/topology-spread-constraint.md)
- [Node Affinity](scheduling/node-affinity.md)
- [Inter-Pod Affinity](scheduling/inter-pod-affinity.md)
