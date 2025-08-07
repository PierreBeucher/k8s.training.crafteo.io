# Node Affinity et Anti-Affinity

Affinity et Anti-affinity existent en deux variantes:

> `requiredDuringSchedulingIgnoredDuringExecution` : le scheduler ne peut pas programmer le Pod si la règle n'est pas respectée. Fonctionne comme `nodeSelector`, mais avec une syntaxe plus expressive.
> `preferredDuringSchedulingIgnoredDuringExecution` : le scheduler essaie de trouver un node qui respecte la règle. Si aucun node ne correspond, le Pod est quand même programmé.

Source : [doc officielle](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

En résumé :
- `requiredDuringSchedulingIgnoredDuringExecution` = **contrainte forte** : le Pod ne sera pas programmé si la contrainte n'est pas respectée
- `preferredDuringSchedulingIgnoredDuringExecution` = **contrainte souple** : le Pod est préféré sur les nodes qui respectent la contrainte, mais sera programmé ailleurs si besoin

On peut définir les deux en même temps pour des comportements complexes.

Exemple: Node Affinity qui exige qu'un Pod soit schedulé dans une zone spécifique, comme un Node Selector:

```yml
spec:
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
             - matchExpressions:
                 - key: "topology.kubernetes.io/zone"
                   operator: In
                   values:
                     - "eu-west-3b"
```

Mettre à jour le Deployment Vote pour :
- Préférer programmer les Pods dans la zone `eu-west-3b` (utiliser `preferred` au lieu de `required`)
- Si le Deployment ou les Pods sont bloqués, supprimer le Deployment et le recréer

Appliquer les changements et observer le comportement du scheduling. Supprimer tous les Pods Vote et observer leur scheduling.

Ajouter une seconde règle pour que le Pod :
- Préfère la zone `eu-west-3b` avec un `weight` de `100`
- Préfère la zone `eu-west-3a` avec un `weight` de `50`
- Observer le résultat
