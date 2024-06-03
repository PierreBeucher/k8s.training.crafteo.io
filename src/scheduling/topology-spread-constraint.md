# Topology Spread Constraint

[Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) allow you to spread workload across domains. It's useful to better achieve HA while being easier to use than Affinity. 

`topologySpreadConstraints` uses `topologyKey` to spread Pods around the domains matching given key, for example:

```yaml
    topologySpreadConstraints:
      - maxSkew: 1
        topologyKey: topology.kubernetes.io/zone
        whenUnsatisfiable: DoNotSchedule
        labelSelector:
          matchLabels:
            app: vote
```

Will spread Vote Pods across the Zone Domain. 

Update Vote Deployment to even loads in current region. 

What's the behavior of `topologySpreadConstraints` in relation to Node/Pod Affinity ? 