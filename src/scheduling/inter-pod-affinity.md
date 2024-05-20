# Inter-pod Affinity and Anti-affinity 

> Inter-pod affinity and anti-affinity allow you to constrain which nodes your Pods can be scheduled on based on the labels of Pods already running on that node, instead of the node labels.

Source: [official doc](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

Inter-pod anti-affinity:
- Configure Redis Deployment to **prefer** scheduling on Nodes without a Redis Pod already running.

Inter-pod affinity:
- Configure Vote Deployment to **require** scheduling on a Node which already have a Redis Pod (for communication optimization) and **prefer** a Node which doesn't already have a Vote Pod. 

Play with replicas on Redis and Vote deployment to observe results.