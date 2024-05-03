# Ingresses

Deploy Ingress with Vote configuration:

```
kubectl apply -f resources/ingress.yml
```

- How does the Ingress map domain name `vote.<YOUR_NAME>.k8s.crafteo.io` to Vote Service?
- Add a similar configuration for `result.<YOUR_NAME>.k8s.crafteo.io` and Result Service