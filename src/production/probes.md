# Liveness, Readiness and Startup Probes 

[Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) define behavior to improve health of Pods in various situations.

## Liveness probe

Liveness probe check health of container regularly, restarting it if it fails. Note that the _container_ itself is restarted (killed and recreated), not the Pod. 

Add a Liveness Probe on Vote container such as:

```yml
        livenessProbe:
         httpGet:
           path: /
           port: 80
         periodSeconds: 2 # This is normally around ~10s, we use shorter time to observe behavior
```

Apply your changes. This should not have any impact on Pod since this healthcheck works.

To test Liveness behavior, override Vote container `command` such as:

```yaml
        command: ["sleep", "infinity"]
```

This will cause Liveness probe to fail since, instead of starting Vote server, container will run a sleep command. Apply and observe behavior (use `kubectl describe` to show events)

Update liveness probe to start 10s after container initial start with a failure theshold of 8.

## Readiness probe

Add a Readiness Probe on Vote container (keep the Liveness Probe). Use a similar method as before to test behavior.

Describe Vote service and verify that no traffic is routed to non-Ready Pod. 

## Startup probe

Add a Startup Probe on Vote container (keep Liveness and Readiness Probes). Use a similar method as before to test behavior.