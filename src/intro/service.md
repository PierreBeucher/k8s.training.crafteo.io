# Service: diriger les flux réseaux vers nos Pods

Manager des Services avec des manifests et accéder à un Pod via un Service:

- Créer un Service avec `kubectl` en utilisant le manifest `intro/service.yml`
  - Rappel : `kubectl apply -f ...`
- Utiliser `kubectl port-forward` pour exposer le service localement et tester l'accès
  - Le port forwarding va _rediriger_ un port local vers votre Pod. Utilisez `curl localhost:PORT` ou équivalent.
  - `kubectl port-forward --help` ou consulter la documentation officielle
- Comment un Service identifie-t-il les Pods à servir ?

---

- Supprimer Pods, Deployment et Service avec une seule commande `kubectl`
- Ré-appliquer notre Deployment, Service et Pod avec une seule commande