# Jobs et CronJobs

Utiliser un CronJob pour voter chaque minute (oui, c'est de la triche)

## Déployer un CronJob

- Déployer le CronJob `resources/cronjob.yml`
- Analyser le contenu du template CronJob. Pourquoi `spec` est-il spécifié plusieurs fois ?
- Quand sera executé le CronJob ?

## Parallélisme

Mettre à jour le CronJob pour lancer 3 instances de Jobs au lieu d'une seule lors du trigger du CronJob.

## Déclencher un Job manuellement à la demande

Lancer une commande `kubectl` pour déclencher manuellement un Job à partir du CronJob sans attendre la prochaine exécution planifiée.
- Utiliser `kubectl create [...]`