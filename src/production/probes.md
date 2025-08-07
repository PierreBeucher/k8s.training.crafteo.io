# Liveness, Readiness et Startup Probes

[Liveness, Readiness et Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) définissent des comportements pour gérer le routage du traffic réseau et auto-réparer les Pods et containers en cas de problèmes (comme une boucle infini ou un blocage d'une application qui n'a pas fait crasher le pod)

## Liveness probe

La liveness probe vérifie régulièrement l'état du container et le redémarre en cas d'échec. Note : c'est le _container_ qui est redémarré (tué et recréé), pas le Pod.

Ajouter une Liveness Probe sur le container Vote, par exemple :

```yml
        livenessProbe:
         httpGet:
           path: /
           port: 80
         periodSeconds: 2 # Normalement ~10s, ici plus court pour observer le comportement
```

Appliquer les changements.

Pour tester le comportement, overrider la commande du container Vote:

```yaml
        command: ["sleep", "infinity"]
```

Cela va faire échouer la Liveness probe car le serveur Vote ne démarre pas, `GET /` ne fonctionnera donc pas. Appliquer et observer le comportement (`kubectl describe` pour voir les events).

Mettre à jour la liveness probe pour démarrer 10s après le démarrage du container, pour fail après 8 tentatives.

## Readiness probe

Ajouter une Readiness Probe sur le container Vote (garder la Liveness Probe). Utiliser une méthode similaire pour tester le comportement.

Décrire le service Vote et vérifier qu'aucun trafic n'est routé vers un Pod non-Ready (dont la Readiness probe échoue).

## Startup probe

Ajouter une Startup Probe sur le container Vote (garder Liveness et Readiness). Utiliser une méthode similaire pour tester le comportement.