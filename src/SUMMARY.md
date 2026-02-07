# Sommaire

[Crafteo - Formation Kubernetes](welcome.md)

# Introduction

- [Notre premier Pod](intro/pod.md)
- [Deployment](intro/deployment.md)
- [Service](intro/service.md)
- [Logs, exec et autres opérations](intro/logs-exec-others.md)

# Controllers

- [Deployments & ReplicaSets](controllers/deployments.md)
- [Jobs & CronJobs](controllers/jobs.md)
- [DaemonSets](controllers/daemonsets.md)
- [StatefulSets](controllers/statefulsets.md)

# Services & Réseau

- [NodePort](services/nodeport.md)
- [LoadBalancer](services/loadbalancers.md)
- [Ingresses et Ingress Controllers](services/ingresses.md)
- [ExternalName Services](services/externalname.md)
- [Avancé: Endpoints, Headless Service...](services/advanced.md)

# Configs & Secrets

- [ConfigMap](config/configmap.md)
- [Secret](config/secret.md)

# Volumes : Persistants & Éphémères

- [Volumes persistants: PVC & PV](volumes/pvc.md)
- [Volumes éphémères: emptyDir](volumes/emptydir.md)

# Outils de déploiement

- [Helm: introduction](deploy-tools/helm-intro.md)
- [Helm: avancé](deploy-tools/helm-advanced.md)
- [Kustomize](deploy-tools/kustomize.md)

# Déploiement en production

- [Ingress & TLS / HTTPS](production/tls.md)
- [Resources Request & Limits](production/resources.md)
- [Horizontal Pod Autoscaler](production/horizontal-scaling.md)
- [Vertical Pod Autoscaler](production/vertical-scaling.md)
- [Liveness, Readiness et Startup Probes](production/probes.md)
- [Pod Disruption Budget (PDB)](production/pdb.md)

# Scheduling

- [Introduction](scheduling/intro.md)
- [Topology Spread Constraint](scheduling/topology-spread-constraint.md)
- [Node Affinity](scheduling/node-affinity.md)
- [Pod Affinity](scheduling/inter-pod-affinity.md)

# Rancher

- [Apps and Helm Charts](rancher/apps.md)
- [CLI](rancher/cli.md)
- [GitOps](rancher/gitops.md)
- [Backup](rancher/backup.md)