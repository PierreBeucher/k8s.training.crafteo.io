# Pod Affinity et Anti-affinity

> Pod affinity et Anti-affinity permettent de contraindre sur quels nodes vos Pods peuvent être schedulés en fonction des labels des Pods déjà présents sur ce node, au lieu des labels du node. Bien que complexe à utiliser, ils permettent des schémas de scheduling avancés. 

Source : [doc officielle](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

## Répartir les Pods sur les Nodes

Contexte: on souhaite répartir les Pods Vote sur les nodes pour équilibrer la charge et améliorer la redondance et la résilience.

Exemple: scheduler les Pods Vote sur un Node qui n'a pas déjà un Pod Vote via une Pod Anti-affinity:

```yml
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          # Groupe les Nodes par Hostname (donc 1 noeud par groupe)
          # Selectionne un groupe (donc un Node) qui n'a pas de Pod matchant le label "app=vote"
          - topologyKey: "kubernetes.io/hostname"
            labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - vote
            namespaceSelector:
              matchExpressions:
              - key: kubernetes.io/metadata.name
                operator: In
                values:
                  - <YOUR NAME>
```

Appliquer au Deployment Vote et observer le résultat.

Cependant, si chaque Node a déjà un Pod Vote, cette contrainte empêchera de programmer de nouveaux Pods Vote. Modifier la contrainte pour utiliser `preferredDuringSchedulingIgnoredDuringExecution` afin de répartir les Pods Vote sur les Nodes sans bloquer: `preferred` vs.  `required`

## Déployer des Pods sur un même Node

Contexte: pour de meilleures performances, on veut que les Pods Redis soient au plus proche des Pods Vote, en préférant répartir les Pods Redis sur les Nodes et en préférant que ces Pods Vote soient déployés sur un Node qui a déjà un Pod Redis (pour réduire la latence réseau en contactant Redis).

Pod anti-affinity :
- Configurer le Deployment Redis pour **préférer** être programmé sur un Node sans Pod Redis déjà présent.

Pod affinity :
- Configurer le Deployment Vote pour **exiger** d'être programmé sur un Node qui a déjà un Pod Redis (pour optimiser la communication) et **préférer** un Node qui n'a pas déjà un Pod Vote.

Jouer avec les replicas sur les Deployments Redis et Vote pour observer les résultats.