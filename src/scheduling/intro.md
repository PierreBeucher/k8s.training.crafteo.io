# Pod scheduling: introduction

Pod scheduling allow to specify Nodes constraints on which Pod will be scheduled. See [official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)

## Node selector: affect Pods directly to Node(s)

Use `nodeSelector` to assign Vote Deployment's Pods to a given Node using the `kubernetes.io/hostname` label.
- Use `kubectl describe node` to identify suitable Node labels
- Update Vote Deployment to defne `nodeSelector` and apply

## Affinity and anti-affinity

Affinity and Anti-affinity comes in two flavors, as per doc:

> `requiredDuringSchedulingIgnoredDuringExecution`: The scheduler can't schedule the Pod unless the rule is met. This functions like nodeSelector, but with a more expressive syntax.
> `preferredDuringSchedulingIgnoredDuringExecution`: The scheduler tries to find a node that meets the rule. If a matching node is not available, the scheduler still schedules the Pod.

In short:
- `requiredDuringSchedulingIgnoredDuringExecution` is a **hard** constraint: Pod won't be scheduled unless constraint is met
- `preferredDuringSchedulingIgnoredDuringExecution` is a **soft** constraint: Pod is prefered to meet criterias, but will be scheduled nonetheless if not met.

Both `required` and `preferred` can be set at the same time for complex behavior.

For example, this define a Pod affinity requiring a Pod to be schedule on a specific Node, reproducing a behavior similar to Node Selector

```yml
spec:
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
             - matchExpressions:
                 - key: "kubernetes.io/hostname"
                   operator: In
                   values:
                     - "ip-192-168-1-189.eu-west-3.compute.internal"
```

Update Vote Deployment to:
- Require Pods to be scheduled in Zone `eu-west-3b` (use label `topology.kubernetes.io/zone: eu-west-3b`)
- Prefer Pods to be scheduled on a specific `kubernetes.io/hostname`
- If your Deployment or Pods are stuck fo some reason, delete Deployment and and re-create it

Apply changes and observe Pod scheduling behavior. Destroy all Vote's Pods and observe their scheduling. 