# Deployment : gérer plusieurs Pods

Un Deployment gère un ensemble de Pods.

- Créer un Deployment avec `kubectl` à partir du manifest `intro/deployment.yml`.
  - Utiliser `kubectl --help`, un moteur de recherche ou une IA si besoin
  - La commande ressemble à `kubectl apply [...]`
- Lister les Deployments avec `kubectl get`
- Redémarrer le Pod créé par notre Deployment
  - Il n'y a pas de commande `restart`, trouver une autre méthode
- Mettre à jour votre Deployment pour avoir 3 replicas de notre Pod