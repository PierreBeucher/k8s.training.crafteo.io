# `logs`, `exec` et autres opérations

De nombreuses commandes `kubectl` sont l'équivalent direct de la CLI `docker` / `podman` sur Kubernetes.

- Afficher les logs d'un de vos Pods en cours d'exécution
  - Équivalent de `docker logs`
  - Vous pouvez aussi cibler un Deployment ou un Service
- Lancer un shell `sh` dans le conteneur d'un Pod
  - Équivalent de `docker exec -it [container] sh`
  - Depuis votre nouveau shell, essayez d'atteindre un autre Pod via son le nom de domaine associé à son Service (ex : `curl <service>.<namespace>.svc.cluster.local`) en spécifiant le port approprié.
- Afficher un Deployment (ou autre object) au format YAML
  - Utilisez une option de `kubectl get`
- Décrire un Deployment
  - Équivalent de `docker inspect`