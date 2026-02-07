# Rancher CLI : utiliser Rancher en ligne de commande

La CLI Rancher permet d'interagir avec Rancher et directement depuis un terminal.

## Créer une clé API

- Accéder à l'interface Rancher à l'adresse https://rancher.k8s.crafteo.io
- Créer une nouvelle clé API (API Key)
  - Le **Bearer Token** sera utilisé pour s'authentifier
- Se connecter à Rancher: `rancher login`

## Utiliser `rancher`

Rancher CLI fournit des sous-commandes `kubectl` qui permettent d'interagir avec vos clusters :

- Lancer des commandes `kubectl` directement avec `rancher`
- Lister les clusters et projets disponibles
- Générer un `kubeconfig` pour votre cluster
- Lister le workload Rancher
- Lister vos clusters et inspecter l'un d'eux
