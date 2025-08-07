# Scalabilité horizontale et Horizontal Pod Autoscaler (HPA)

Configurer un Horizontal Pod Autoscaler (HPA) pour scaler automatiquement les Pods Vote lorsque leur charge CPU est élevée. On utilisera un Pod Auto Voter pour simuler une charge CPU (beaucoup de votes !)

Mettre à jour le Deployment Vote pour spécifier les ressources et requests:

```yaml
        resources:
          requests:
            cpu: 50m
            memory: 128Mi
          limits:
            cpu: 100m
            memory: 256Mi
```

Déployer Auto Voter : `kubectl apply -f resources/scaling/auto-voter.yml`
- C'est une simple boucle bash qui envoie des requêtes POST au service Vote.
- Observer la charge CPU de Vote avec la commande `kubectl top` (CPU idle ~2m, devrait passer à ~50m). Exemple :
```sh
watch kubectl top pod vote-xxx
```

Déployer le HPA dans `resources/scaling/hpa.yml` et observer la scalabilité
- Comment le HPA sait-il quand scaler un pod ?

Supprimer Auto Voter et observer le HPA réduire le nombre de pods. 
  