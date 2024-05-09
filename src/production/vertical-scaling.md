# Vertical Scalability and Cluster Autoscaler

The Cluster Autoscaler is responsible to continuously observe cluster state and add or remove nodes as needed. It uses resources requests and Pod scheduling capacity to identify when to add or remove nodes.

Configure Vote deployment to have resources such as:

```yaml
        resources:
          requests:
            cpu: 500m
            memory: 512Mi
          limits:
            cpu: 1000m
            memory: 1024Mi
```

Then scale Vote deployment to have 20 Pods

```sh
kubectl scale deployment vote --replicas 20
```

Observe Pod behavior:
- Pods are scheduled and remain Pending
- New nodes are added to make more room for new Pods (up to a certain maximum)

Then scale back your Deployment to 1
- Observe Nodes are removed

Identify the Cluster Autoscaler in `kube-system` responsible for autoscaling. 