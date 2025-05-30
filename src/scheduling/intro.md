# Pod scheduling: introduction

Pod scheduling allow to specify Nodes constraints on which Pod will be scheduled. See [official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)

## Node selector: affect Pods using Node labels

Kubernetes Nodes have labels like other Kubernetes objects. You can get Node labels by `get`ing or `describe`ing a Node.

```sh
kubectl get node some-node-name -o yaml
```
```yaml
apiVersion: v1
kind: Node
metadata:
  name: some-node-name

  # These labels can be used by Pods to select Nodes
  # Much like Services use labelSelector to select Pods
  labels:
    beta.kubernetes.io/arch: amd64
    beta.kubernetes.io/os: linux
    kubernetes.io/hostname: some-node-name
    topology.kubernetes.io/region: us-central1
    topology.kubernetes.io/zone: us-central1-a

# ...
```

Use `nodeSelector` to assign Vote Deployment's Pods to a given Node using the `topology.kubernetes.io/zone` label.
- Use `kubectl describe node` or `kubectl get node -o yaml` to identify suitable Node labels
- Update Vote Deployment to define `nodeSelector` and apply

## Affect Pods to specific Nodes

Use a Pod's `nodeName` to assign a Pod to a specific Node.