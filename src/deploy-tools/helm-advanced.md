# Helm avancé: écrire un chart Helm

Le dossier `resources/helm/example-voting-app` contient un chart Helm avec des manifests YAML templatisés.

## Déploiement, mise à jour et values

Utiliser la commande `helm install` pour déployer un release du chart Example Voting App.
- Vérifier le fonctionnement via un port-forward
- Explorer les templates YAML pour comprendre le mécanisme de templating et le lien avec `values.yml`

Il est possible d'override `values.yml` avec des fichiers de configuration externes, typiquement par environnement.
- Mettre à jour le release pour surcharger les valeurs par défaut avec `resources/helm/values/dev.yml`

## Gestion des Secrets

Helm ne fournit pas de mécanisme natif pour gérer les secrets. Un pattern courant est de référencer un secret externe (non géré par le chart).

Mettre à jour le release Helm en utilisant les valeurs de `resources/helm/values/prod.yml`.
- Cette configuration référence un secret externe, **il faut le créer soi-même**
- Explorer le contenu du chart pour comprendre le mécanisme sous-jacent

Il existe aussi des [plugins Helm](https://helm.sh/docs/topics/plugins/) permettant la gestion des secrets comme [`helm-secrets`](https://github.com/jkroepke/helm-secrets)