# ConfigMap

Les ConfigMap sont utilisées pour monter des configurations ou des variables d'environnement dans les containers.

## Variables d'environnement

Le déploiement Database définit des variables d'environnement pour l'utilisateur et le mot de passe Postgres. Remplacer ces variables par celles définies dans la ConfigMap `resources/config/configmap-postgres-env.yml`

- Créer la ConfigMap avec `kubectl apply`
- Mettre à jour le Deployment pour utiliser la ConfigMap afin de charger les variables d'environnement. Utiliser quelque chose comme ceci dans le template du Pod :
```yaml
    envFrom:
    - configMapRef:
        name: db-env
```

## Fichiers de configs

Utiliser la ConfigMap `resources/config/configmap-postgres-config.yml` pour monter une configuration Postgres personnalisée dans le container à `/etc/postgresql/postgresql.conf`
- Équivalent de `docker run -v "$PWD/my-postgres.conf":/etc/postgresql/postgresql.conf`

Utiliser quelque chose comme ceci dans le spec du Pod :

```yaml
    spec:
      # [...]
      containers:
      - name: postgres
        # [...]
        # Utiliser un fichier de config personnalisé
        args: [ "-c", "config_file=/etc/postgresql/postgresql.conf"]
        # Monter la config personnalisée dans le container
        volumeMounts:
        - mountPath: /etc/postgresql
          name: config-vol
      volumes:
      - name: config-vol
        configMap:
          name: db-config
```