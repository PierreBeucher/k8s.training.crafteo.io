# Pod scheduling: introduction

Pod scheduling allow to specify Nodes constraints on which Pod will be scheduled. See [official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)

It's set via Pod `spec` or `specTemplate`, for example to restrict scheduling on Node with desired labels (only deploy Pod in France zone):

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: topology.kubernetes.io/zone
          operator: In
          values:
          - francecentral-1
          - francecentral-2
```

## Node selector: affect Pods directly to Node(s)

Use `nodeSelector` to assign Vote Deployment's Pods to a given Node using the `kubernetes.io/hostname` label.
- Use `kubectl describe node` to identify suotable Node labels
- Update Vote Deployment to defne `nodeSelector` and apply


## Affinity and anti-affinity

Affinity and Anti-affinity comes in two flavors, as per doc:

> `requiredDuringSchedulingIgnoredDuringExecution`: The scheduler can't schedule the Pod unless the rule is met. This functions like nodeSelector, but with a more expressive syntax.
> `preferredDuringSchedulingIgnoredDuringExecution`: The scheduler tries to find a node that meets the rule. If a matching node is not available, the scheduler still schedules the Pod.

In short:
- `requiredDuringSchedulingIgnoredDuringExecution` is a **hard** constraint: Pod won't be scheduled unless constraint is met
- `preferredDuringSchedulingIgnoredDuringExecution` is a **soft** constraint: Pod is prefered to meet criterias, but will be scheduled nonetheless if not met.

Both can be set at the same time for complex behavior.

Update Vote Deployment to:
- Require Pods to be scheduled in Region `eu-west-3`
- Prefer Pods to be scheduled on a specific `kubernetes.io/hostname`

Apply changes and observe Pod scheduling behavior.