# Scalabilité verticale et Cluster Autoscaler

Le Cluster Autoscaler observe en continu l'état du cluster et ajoute ou retire des Nodes selon le besoin. Il utilise les requests de ressources et la capacité de scheduling des Pods pour décider d'ajouter ou retirer des Nodes. 

Configurer le deployment Vote pour avoir les ressources suivantes :

```yaml
        resources:
          requests:
            cpu: 500m
            memory: 512Mi
          limits:
            cpu: 1000m
            memory: 1024Mi
```

Scaler ensuite le deployment Vote à 20 Pods

```sh
kubectl scale deployment vote --replicas 20
```

Observer le comportement des Pods :
- Les Pods sont en Pending
- De nouveaux nodes sont ajoutés pour accueillir les nouveaux Pods (jusqu'à un certain maximum)

Revenir à 1 replica
- Observer la suppression des nodes

Identifier le Cluster Autoscaler dans `kube-system` responsable de l'autoscaling. 