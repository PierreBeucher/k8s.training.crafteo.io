# Deployments

## Update replica count

- List Deployments with `kubectl`. Identify the ReplicaSet associated to Vote Deployment. 
- Update Vote deployment to 3 replicas. Observe ReplicaSet state.
  - You can `apply` directly or use `kubectl edit`
- Update Vote deployment back to 1 replica. Observe ReplicaSet state.

## Deployment and Pods

How does a Deployment identify which Pods it must manage?

## Deployment rollout and rollback

Update Vote deployment image to a non-existing image (make it fail on purpose).

- Use `kubectl rollout status` to observe deployment in progress.
- Observe ReplicaSet state. 
- Use another command of `kubectl rollout` to rollback buggy deployment.

## Strategy

By default, a Deployment update strategy is RollingUpdate. 

- Find other Deployment strategies
- Update Vote deployment to use this strategy and test it