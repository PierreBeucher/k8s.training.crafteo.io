# Ingresses

Deploy Ingress with Vote configuration:

```
kubectl apply -f resources/ingress.yml
```

- How does the Ingress map domain name `vote.<YOUR_NAME>.k8s.crafteo.io` to Vote Service?
- Add a similar configuration for `result.<YOUR_NAME>.k8s.crafteo.io` and Result Service

## Ingress Controller

An Ingress does not work by its own - it needs an Ingress Controller. 

Traefik is currently deployed and act as Ingress Controller:
- Identify the LoadBalancer service used by Traefik
- Is it possible to deploy multiple Ingress Controllers ? 