# ConfigMap

ConfigMap are used to mount configurations or environment variables in Pods and containers.

# Environment variables

Use ConfigMap `resources/config/configmap-postgres-env.yml` to replace plain environment variables in Deployment
- Equivalent of `docker run --env-file`

Use something like this in Pod template:

```yaml
    envFrom:
    - configMapRef:
        name: db-env
```

# Files as Volumes

Use ConfigMap `resources/config/configmap-postgres-config.yml` to mount a custom Postgres configuration in container at `/etc/postgresql/postgresql.conf`
- Equivalent of `docker run -v "$PWD/my-postgres.conf":/etc/postgresql/postgresql.conf`

Use something lik this in Pod spec:

```yaml
    spec:
      # [...]
      containers:
      - name: postgres
        # [...]
        volumeMounts:
        - mountPath: /var/lib/postgresql/data/postgresql.conf
          name: config-vol
          subPath: postgresql.conf
      volumes:
      - name: config-vol
        configMap:
          name: db-config
```