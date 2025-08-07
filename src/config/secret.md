# Secret

Les Secrets sont similaires aux ConfigMaps, sauf qu'ils sont (théoriquement) chiffrés dans le Control Plane. Leur accès et utilisation doivent être protégés avec une autorisation appropriée dans le cluster.

Les Secrets nécessitent que leur configuration soit encodée en Base64. Utiliser une commande pour encoder une chaîne en Base64 :

```
echo -n "mypassword" | base64
```

_Note : Base64 n'est PAS un chiffrement. Il ne doit pas être utilisé pour protéger un secret. Base64 est utilisé car les secrets peuvent contenir des données binaires et leur représentation base64 peut être utilisée comme chaîne de caractères._

# Utiliser une chaîne en clair dans un Secret ?

Par défaut, les valeurs des secrets doivent être encodées en base64, ex :

```yaml
data:
    # "secretPassword" en base 64
    password: c2VjcmV0UGFzc3dvcmQ=
```

Trouver un moyen d'utiliser des chaînes en clair au lieu de données encodées en base64 dans un manifest YAML Secret.

# Variables d'environnement depuis un Secret

Utiliser le Secret `resources/config/secret-postgres-env.yml` pour définir des variables d'environnement dans le Deployment Postgres

# Fichiers depuis un Secret

Copier la ConfigMap `resources/config/configmap-postgres-config.yml` et la transformer en Secret pour monter une configuration Postgres personnalisée dans le container à `/etc/postgresql/postgresql.conf`

