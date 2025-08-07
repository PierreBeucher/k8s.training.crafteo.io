# ExternalName Services

Créer un service ExternalName pointant vers google.com:

```
kubectl apply -f resources/externalname-service.yml 
```

- Lancer un shell dans le conteneur Vote avec `kubectl exec`
- Essayer de `curl https://external-test` et observer le résultat