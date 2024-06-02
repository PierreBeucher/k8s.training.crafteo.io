# Inter-pod Affinity and Anti-affinity 

> Inter-pod affinity and anti-affinity allow you to constrain which nodes your Pods can be scheduled on based on the labels of Pods already running on that node, instead of the node labels.

Source: [official doc](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

## Spread Pods on Nodes

Context: you want to spread Vote Pods on your nodes to even load and improve redundancy and resilience. 

Prefer scheduling Vote Pods on Node which doesn't already have one using an affinity such as:

```yml
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - topologyKey: "kubernetes.io/hostname"
            labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - vote
            namespaceSelector:
              matchExpressions:
              - key: kubernetes.io/metadata.name
                operator: In
                values:
                  - <YOUR NAME>
```

## Deploy Pods together

Context: for better performance, you want to have Redis Pods as close as possible to Vote Pods by preferring spreading Redis Pods on Nodes and preferring Vote Pods to deploy on a Node already running a Redis Pod (so that cache can be reached on the same Node, reducing network latency). 

Inter-pod anti-affinity:
- Configure Redis Deployment to **prefer** scheduling on Nodes without a Redis Pod already running.

Inter-pod affinity:
- Configure Vote Deployment to **require** scheduling on a Node which already have a Redis Pod (for communication optimization) and **prefer** a Node which doesn't already have a Vote Pod. 

Play with replicas on Redis and Vote deployment to observe results.