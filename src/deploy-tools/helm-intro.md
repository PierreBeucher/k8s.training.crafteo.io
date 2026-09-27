# Helm : package manager pour Kubernetes

[Helm](https://helm.sh/) est un "package manager" pour Kubernetes. Il utilise des templates YAML pour gérer les ressources Kubernetes et permet de partager des "Charts" publiques ou privées. 

On trouve des charts Helm sur [Artifact Hub](https://artifacthub.io/) ou via n'importe quel moteur de recherche.

Exemple d'utilisation :

```sh
helm --help

# Installer un chart Redis
# 'myredis' est le nom du Release (comme un nom de container pour une image)
# 'bitnami/redis' est le chart à installer
helm install my-redis oci://registry-1.docker.io/bitnamicharts/redis
```

Ajouter un repository n'est pas toujours nécessaire, de nombreuses charts sont aujourd'hui installables via OCI comme:

```sh
helm install my-redis oci://registry-1.docker.io/bitnamicharts/redis
```

## Installer un chart Wordpress

Trouver un chart Wordpress et l'installer. Essayer d'y accéder en externe avec un port-forward.
- Wordpress est un système de blog avec une base de données. Il fournit un frontend simple à atteindre depuis internet.
- Chercher un chart Wordpress par n'importe quelle méthode

Une fois terminé, désinstaller le release du chart Wordpress
