# StatefulSets

Déployer une base de données Postgres en StatefulSet avec la commande :

```
helm install my-postgres oci://registry-1.docker.io/bitnamicharts/postgresql -f resources/postgres-sts-values.yml
```

Cette commande crée plusieurs StatefulSets. _Note : Helm est un package manager pour Kubernetes, l'équivalent de `apt` ou `yum` pour Linux. On reviendra sur Helm plus tard._

- Utiliser `kubectl` pour décrire les Pods et PersistentVolumes. Observer le nommage des pods.
- Supprimer un Pod et observer le résultat.
- Supprimer le release Helm Postgres avec `helm delete my-postgres`. Que se passe-t-il pour les volumes ?