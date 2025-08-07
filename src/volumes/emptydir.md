# emptyDir volume

`emptyDir` peut être utilisé dans différentes situations, comme partager des données entre les containers d'un même Pod. Par exemple pour créer une sauvegarde d'une base de données:
- Configurer un Pod avec 2 containers,  `postgres` (dump database) et `aws` (upload de données)
- Partager un volume `/backup` entre les 2 containers d'un même Pod pour "passer" le dump de `postgres` à `aws`

Un CronJob de backup est présent dans `resources/volumes/cronjob.yml` mais il manque la configuration des Volumes. Adapter le template pour :

- Déclarer un volume `emptyDir` (utiliser `volumes:` au bon endroit)
  - Le volume doit être déclaré au niveau du Pod puis un point de montage effectué au niveau de chaque container
- Monter le volume sur le path `/backup` pour les deux containers
- Créer le CronJob et le déclencher (créer un Job à partir du CronJob) avec
  ```sh
  kubectl create job --from=cronjob/postgres-backup manual-backup
  ```
- Observer le résultat 