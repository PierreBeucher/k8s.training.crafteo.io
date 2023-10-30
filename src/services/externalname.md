# ExternalName Services

Create an ExternalName service pointing to google.com:

```
kubectl apply -f resources/externalname-service.yml 
```

- Run a shell in the Vote container with `kubectl exec`
- Try to `curl https://external-test` and observe result