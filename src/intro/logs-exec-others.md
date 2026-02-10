# `logs`, `exec` et autres opérations

De nombreuses commandes `kubectl` sont l'équivalent direct de la CLI `docker` / `podman` sur Kubernetes.

- Afficher les logs d'un de vos Pods en cours d'exécution
  - Équivalent de `docker logs`
  - Vous pouvez aussi cibler un Deployment ou un Service
- Lancer un shell `sh` dans le conteneur d'un Pod
  - Équivalent de `docker exec -it [container] sh`
  - Utile pour débugger le comportement d'un Pod et ses containers!
- Afficher un Deployment (ou autre object) au format YAML
  - Utilisez une option de `kubectl get`
- Décrire un Deployment
  - Équivalent de `docker inspect`