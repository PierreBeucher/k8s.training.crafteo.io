# Ingresses

Déployer un Ingress avec la configuration Vote :

```
kubectl apply -f resources/ingress.yml
```

- Comment l'Ingress fait-il le lien entre le nom de domaine `vote.<YOUR_NAME>.k8s.crafteo.io` et le Service Vote ?
- Ajouter une configuration similaire pour `result.<YOUR_NAME>.k8s.crafteo.io` et le Service Result

## Ingress Controller

Un Ingress ne fonctionne pas tout seul – il a besoin d'un Ingress Controller.

Traefik est actuellement déployé et agit comme Ingress Controller:
- Identifier le service LoadBalancer utilisé par Traefik
- Est-il possible de déployer plusieurs Ingress Controllers ? 