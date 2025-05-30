# Topology Spread Constraint

[Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) allow you to spread workload across domains using topology. It's useful to **better achieve HA and resilience** by spreading Pods across multiple zones, regions, etc.

`topologySpreadConstraints` uses `topologyKey` to spread Pods around the domains matching given key, for example:

```yaml
    topologySpreadConstraints:
      # Maximum difference between two domains, 
      # eg. a domain cannot have more than 1 Pod than another domain
      - maxSkew: 1

        # Topology key used to define domain
        # Pods will be spread across different zones
        topologyKey: topology.kubernetes.io/zone
        
        # Behavior if constraint cannot be respected
        whenUnsatisfiable: DoNotSchedule

        # Only Pods matching these labels will be constrained
        labelSelector:
          matchLabels:
            app: vote

```

Update Vote Deployment to even loads in current region. 

What's the behavior of `topologySpreadConstraints` in relation to Node/Pod Affinity ? 