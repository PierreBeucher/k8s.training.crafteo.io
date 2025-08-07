# Pod Resources / Requests

Les Pods peuvent avoir des [requests et limits de ressources](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/), par exemple:

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

Affecter des ressources à vos Pods :
- Mettre à jour les Pods Vote pour demander 1 CPU et 1024Mi de mémoire
- Quelles unités peut-on utiliser pour spécifier les ressources ? Quelle différence entre `128M` et `128Mi` ?

Requests et limits affectent le scheduling différemment. Mettre les ressources des Pods Vote comme ci-dessous et scaler à 10 replicas. Observer le résultat.

```yml
resources:
  requests:
    cpu: 1m
    memory: 2Mi
  limits:
    cpu: 1
    memory: 1Gi
```

Mettre ensuite les ressources comme ci-dessous, scaler à 10 replicas et observer le résultat.

```yml
resources:
  requests:
    cpu: 250m
    memory: 256Mi
  limits:
    cpu: 1
    memory: 1Gi
```
