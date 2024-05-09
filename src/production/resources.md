# Pod Resources / Requests

Pods can have [resources requests and limits](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) such as:

```yaml
spec:
  template:
    spec:
      containers:
      - name: # ...
        resources:
          requests:
            cpu: 1
            memory: "1Gi"
          limits:
            cpu: 2
            memory: 2Gi
```

Affect resources to your Pods:
- Update Vote Pods to request 1 CPU and 1024Mi memory and apply
- Update Vote Pods to request 0.2 CPU and 128Mi memory and apply
- What units can you use to specify resources and requests ? What's the difference between `128M` and `128Mi` ?

Requests and limits affect scheduling differently. Set Vote's Pods resources as below and scale to 10 replicas. Observe result.

```yml
resources:
  requests:
    cpu: 1m
    memory: 2Mi
  limits:
    cpu: 1
    memory: 1Gi
```

Now set resources as below and scale to 10 replicas and observe result.

```yml
resources:
  requests:
    cpu: 250m
    memory: 256Mi
  limits:
    cpu: 1
    memory: 1Gi
```
