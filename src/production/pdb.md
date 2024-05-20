# Pod Disruption Budget (PDB)

Pod Disruption Budget (PDB) are used to specify how much Pod can become unavailable during an update. See [official doc](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)

Update Vote Deployment to have 5 replicas, a Readiness Probe and prefer Pods to be deployed on a single node, eg:

```yml
apiVersion: apps/v1
kind: Deployment
# ...
spec:
  replicas: 5
  template:
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
            - weight: 100
              preference:
                matchExpressions:
                  - key: "kubernetes.io/hostname"
                    operator: In
                    values:
                      - "ip-192-168-1-4.eu-west-3.compute.internal"
      containers:
      - name: vote
        # ...
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
```

Create a PDB for Vote to allow max 1 Pod unavailable such as:

```yml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: vote-pdb
spec:
  minAvailable: 4
  selector:
    matchLabels:
      app: vote
```

Then drain the Node on which you deployed your Pods to observe behavior.

```sh
# Example command to drain a node
# Replaced with your node name
kubectl drain ip-192-168-1-160.eu-west-3.compute.internal --delete-emptydir-data=true --ignore-daemonsets=true
```

Reproduce with `maxUnavailable: 2` instead of `minAvailable: 1`

What happens when you set desired value as percentage and Pod number is not round? (eg. minAvailable of 50% out of 5 replicas)