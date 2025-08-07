# Pod Disruption Budget (PDB)

Les Pod Disruption Budget (PDB) servent à spécifier un nombre de Pods pouvant devenir indisponibles lors d'une mise à jour. Si le PDB ne peut pas être respecté, la mise à jour d'un Deployment ou autre object échouera ou restera bloqué. C'est un méchanisme de sécurité pour empêcher les downtimes involontaires. Voir [la doc officielle](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)

Mettre à jour le Deployment Vote pour avoir 5 replicas, une Readiness Probe et préférer déployer les Pods sur un seul node, ex :

```yml
apiVersion: apps/v1
kind: Deployment
# ...
spec:
  replicas: 5
  template:
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
            - weight: 100
              preference:
                matchExpressions:
                  - key: "kubernetes.io/hostname"
                    operator: In
                    values:
                      - "ip-192-168-1-4.eu-west-3.compute.internal"
      containers:
      - name: vote
        # ...
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
```

Créer un PDB pour Vote pour permettre max 1 Pod indisponible, par exemple :

```yml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: vote-pdb
spec:
  minAvailable: 4
  selector:
    matchLabels:
      app: vote
```

Drainer ensuite le Node sur lequel les Pods sont déployés pour observer le comportement.

```sh
# Exemple de commande pour drainer un node
# Remplacer par le nom de votre node
kubectl drain ip-192-168-1-160.eu-west-3.compute.internal --delete-emptydir-data=true --ignore-daemonsets=true
```

Reproduire avec `maxUnavailable: 2` au lieu de `minAvailable: 1`

Que se passe-t-il si on met une valeur en pourcentage et que le nombre de Pods n'est pas rond ? (ex : minAvailable à 50% sur 5 replicas)
