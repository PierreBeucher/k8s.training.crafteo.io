# Node Affinity and Anti-Affinity

Affinity and Anti-affinity comes in two flavors, as per doc:

> `requiredDuringSchedulingIgnoredDuringExecution`: The scheduler can't schedule the Pod unless the rule is met. This functions like `nodeSelector`, but with a more expressive syntax.
> `preferredDuringSchedulingIgnoredDuringExecution`: The scheduler tries to find a node that meets the rule. If a matching node is not available, the scheduler still schedules the Pod.

Source: [official doc](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)
In short:
- `requiredDuringSchedulingIgnoredDuringExecution` is a **Hard** constraint: Pod won't be scheduled unless constraint is met
- `preferredDuringSchedulingIgnoredDuringExecution` is a **Soft** constraint: Pod is prefered to meet criterias, but will be scheduled nonetheless if not met.

Both `required` and `preferred` can be set at the same time for complex behavior.

For example, this define a Pod affinity requiring a Pod to be scheduled in a specific zone, reproducing a behavior similar to Node Selector

```yml
spec:
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
             - matchExpressions:
                 - key: "topology.kubernetes.io/zone"
                   operator: In
                   values:
                     - "eu-west-3b"
```

Update Vote Deployment to:
- Require Pods to **PREFER** being scheduled in Zone `eu-west-3b` instead of example above using `required`
- If your Deployment or Pods are stuck fo some reason, delete Deployment and and re-create it

Apply changes and observe Pod scheduling behavior. Destroy all Vote's Pods and observe their scheduling. 

Add a second rule so that our Pod:
- Prefer being scheduled in Zone `eu-west-3b` with a `weight` of `100`
- Prefer being scheduled in Zone `eu-west-3a` with a `weight` of `50`
- Observe result
