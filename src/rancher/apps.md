# Rancher Apps : déployer des charts via l'interface

[Rancher](https://rancher.com/) est une plateforme de gestion Kubernetes qui fournit une interface web pour gérer vos clusters et déployer des applications.

Accéder à l'interface Rancher à l'adresse https://rancher.k8s.crafteo.io

## Déployer un chart Monitoring

- Naviguer vers la section **Apps** dans l'interface Rancher
- Rechercher et déployer un chart de **Monitoring**
- Observer les ressources créées par le chart dans votre cluster Kubernetes

Une fois le déploiement terminé, vérifier que les Pods du chart Monitoring sont bien en cours d'exécution avec `kubectl get pods`.

