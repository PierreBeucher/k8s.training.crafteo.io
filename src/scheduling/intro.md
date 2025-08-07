# Contraintes de Scheduling: introduction

Les contraintes de scheduling des Pods permettent de spécifier comment un Pod sera scheduler sur un Node. Voir [la documentation officielle](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)

## Node selector: affecter des Pods via les labels Node

Les Nodes Kubernetes ont des labels comme les autres objets Kubernetes. On peut obtenir les labels d'un Node avec `get` ou `describe`.

```sh
kubectl get node some-node-name -o yaml
```
```yaml
apiVersion: v1
kind: Node
metadata:
  name: some-node-name

  # Ces labels peuvent être utilisés par les Pods pour sélectionner les Nodes
  # Comme les Services utilisent labelSelector pour sélectionner les Pods
  labels:
    beta.kubernetes.io/arch: amd64
    beta.kubernetes.io/os: linux
    kubernetes.io/hostname: some-node-name
    topology.kubernetes.io/region: us-central1
    topology.kubernetes.io/zone: us-central1-a

# ...
```

Utiliser `nodeSelector` pour affecter les Pods du Deployment Vote à un Node donné via le label `topology.kubernetes.io/zone`.
- Utiliser `kubectl describe node` ou `kubectl get node -o yaml` pour identifier les labels des Nodes
- Mettre à jour le Deployment Vote pour définir `nodeSelector` et appliquer

## Affecter un Pod à un Node spécifique

Utiliser le champ `nodeName` d'un Pod pour l'affecter à un Node précis.