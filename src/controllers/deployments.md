# Deployments

## Modifier le nombre de replicas

- Lister les Deployments avec `kubectl`. Identifier le ReplicaSet associé au Deployment Vote.
- Mettre à jour le Deployment Vote à 3 replicas. Observer l'état du ReplicaSet.
  - Appliquer directement ou utiliser `kubectl edit`
- Repasser le Deployment Vote à 1 replica. Observer l'état du ReplicaSet.
- Mettre à jour l'image du Deployment Vote avec un tag inexistant. Observer l'état du ReplicaSet.

## Deployment et Pods

Comment un Deployment identifie-t-il les Pods qu'il manage ?

## Rollout et rollback d'un Deployment

Mettre à jour l'image du Deployment Vote avec une image inexistante (provoquer un échec volontairement).

- Utiliser `kubectl rollout status` pour observer le déploiement en cours.
- Observer l'état du ReplicaSet.
- Utiliser une autre commande de `kubectl rollout` pour rollback le déploiement en échec.

## Stratégie

Par défaut, la stratégie de mise à jour d'un Deployment est RollingUpdate.

- Trouver d'autres stratégies de mise à jour pour les Deployments
- Mettre à jour le Deployment Vote pour utiliser cette stratégie et la tester