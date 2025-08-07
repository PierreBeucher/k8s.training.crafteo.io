# Concepts avancés sur les Services

## Endpoints et EndpointSlices

Les Services utilisent des EndpointSlices (et Endpoints) en interne pour rediriger le trafic.

- Scaler le déploiement Vote à 3 replicas
- Identifier les EndpointSlices et Endpoints créés pour le service Vote

Historiquement, les Endpoints étaient utilisés pour lier les Services aux Pods. Aujourd'hui les EndpointSlices fournissent une API plus complète et remplaceront progressivement les Endpoints. Voir [la doc Kubernetes pour plus de détails](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/#motivation)

## Headless Services

Les Headless Services sont utilisés quand le load balancing n'est pas nécessaire. Les Headless services n'ont pas d'IP.

En utilisant des selectors, une requête DNS interne retournera directement toutes les IPs des pods existants.

- Scaler les déploiements Vote et Service à 3 replicas
- Supprimer le service Vote
- Mettre à jour le template du service Vote avec `spec.clusterIP: "None"`
- Re-déployer le service Vote
- Lancer un shell dans le Pod Vote et observer le comportement DNS entre les services `vote` et `result`. 
  - Lancer un shell dans un container `kubectl exec -it ... sh` et ces commandes pour installer les outils DNS et checker la résolution:
```
# Installer des outils DNS à la volée pour tester
apt update && apt install dns-utils

nslookup vote
nslookup result
```

## Exposition des services dans les Pods

Les services sont exposés aux Pods via des variables d'environnement.

- Lancer un shell dans le pod Vote et explorer les services disponibles
  - Utiliser `env` pour afficher toutes les variables d'environnement, et `env | grep` pour filtrer
- Trouver les variables d'environnement du service Result

L'approche la plus courante est d'utiliser les enregistrements DNS pointant vers les Services.
