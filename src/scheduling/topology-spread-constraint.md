# Topology Spread Constraint

[Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) permettent de répartir la charge sur plusieurs domaines (zones, régions, etc.) topologiques. C'est utile pour **améliorer la haute disponibilité et la résilience** en répartissant les Pods sur plusieurs zones, régions, etc.

`topologySpreadConstraints` utilise `topologyKey` pour répartir les Pods sur les domaines correspondant à la clé, par exemple :

```yaml
    topologySpreadConstraints:
      # Différence maximale entre deux domaines,
      # ex. un domaine ne peut pas avoir plus d'1 Pod qu'un autre
      - maxSkew: 1

        # Clé de topologique utilisée pour définir le domaine
        # Les Pods seront répartis sur différentes zones
        topologyKey: topology.kubernetes.io/zone
        
        # Comportement si la contrainte ne peut pas être respectée
        whenUnsatisfiable: DoNotSchedule

        # Seuls les Pods correspondant à ces labels seront contraints
        labelSelector:
          matchLabels:
            app: vote

```

Mettre à jour le Deployment Vote pour équilibrer la charge dans la région courante.

Quel est le comportement de `topologySpreadConstraints` par rapport à Node/Pod Affinity ? 