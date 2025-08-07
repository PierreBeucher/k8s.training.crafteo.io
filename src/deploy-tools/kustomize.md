# Kustomize

Kustomize est un outil intégré à `kubectl` pour du déploiement multi-environnements et la gestion de configuration.

Voir la [documentation officielle de Kustomize](https://kubectl.docs.kubernetes.io) et la [documentation de référence](https://kubectl.docs.kubernetes.io/references/kustomize/)

## Kustomize Example Voting App

Un déploiement d'application avec Kustomize nécessite:

- Une _base_ avec la config YAML (Deployment, Services, etc.) et un `kustomization.yml` listant les ressources et options souhaitées
- Un ou plusieurs overrides (typiquement par environnement, mais pas forcément)

Pour Kustomizer Example Voting App :

- Copier `resources/kustomize/base-kustomization.yml` dans `base/kustomization.yml`. Ce fichier référence toutes les ressources de l'Example Voting App.
- Utiliser l'un des dossiers `resources/kustomize/dev` ou `resources/kustomize/prod` avec `kubectl`. Chacun référence sa base via un chemin relatif, ex : `resources: [ "../../../base" ]`

```sh
#
# Attention au -k
#
# Comme kubectl apply -f mais va lire depuis dev et toutes les ressources référencées (y compris la base)
kubectl apply -n <YOU> -k resources/kustomize/dev
```

Observer le résultat selon le contenu des fichiers `kustomization.yml` de dev et base, en particulier `commonLabels`

## Définir le namespace

Créer un namespace avec votre nom préfixé par `-kustomize`, ex : `YOU-kustomize`.

Mettre à jour le `kustomization.yml` de dev pour définir le namespace `YOU-kustomize` et appliquer sans flag `-n xxx`, ex :

```sh
kubectl apply -k resources/kustomize/dev
```

Que sont devenues les ressources dans l'ancien namespace ?

## Patches et générateurs ConfigMap/Secret

Utiliser un [ConfigMap generator](https://kubectl.docs.kubernetes.io/guides/config_management/secrets_configmaps/) pour créer une ConfigMap à partir du fichier `postgresql.conf`

Utiliser un [Secret generator](https://kubectl.docs.kubernetes.io/guides/config_management/secrets_configmaps/) pour créer un Secret à partir du fichier `postgres-secret.properties`
- Il faut des options supplémentaires pour considérer ce fichier comme des variables d'environnement

Surcharger le Deployment avec un _patch_ pour s'assurer que les valeurs du Secret et de la ConfigMap sont utilisées à la place de celles définies dans la base.
- Utiliser `db-deployment-patch.yml` et mettre à jour `kustomization.yml`

## Adapter une autre Kustomization

Reproduire les changements de la Kustomization `dev` dans la Kustomization `prod` et déployer les deux dans le même namespace. 