# Horizontal Scalability and Horizontal Pod Autoscaler (HPA)

Let's configure an Horizontal Pod Autoscaler (HPA) to automatically scale our Vote Pods when their CPU load is high. We'll use a Auto Voter Pod to emulate a CPU charge (lots of vote !)

Update Vote deployment to specify resources and requests such as:

```yaml
        resources:
          requests:
            cpu: 50m
            memory: 128Mi
          limits:
            cpu: 100m
            memory: 256Mi
```

Deploy Auto Voter: `kubectl apply -f resources/scaling/auto-voter.yml`
- It's a simple bash loop sending POST request to Vote service.
- Observe Vote CPU load with `kubectl top` command (CPU load is ~2m idle, and should now be around ~50m). For example:
```sh
watch kubectl top pod vote-xxx
```

Deploy HPA in `resources/scaling/hpa.yml` and observe scalability
- How does HPA know when a pod should be scaled-up?

Delete Auto Voter and observe HPA scale down. 
  