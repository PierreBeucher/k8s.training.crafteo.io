# ConfigMap

ConfigMap are used to mount configurations or environment variables in Pods and containers.

# Environment variables

Database Deployment define environment variables for Postgres user and password. Replace them with those defined in ConfigMap `resources/config/configmap-postgres-env.yml`

- Create ConfigMap with `kubectl apply`
- Update Deployment to use ConfigMap to load environment variables.  Use something like this in Pod template:
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
        # Use custom config file
        args: [ "-c", "config_file=/etc/postgresql/postgresql.conf"]
        # Mount custom config in container
        volumeMounts:
        - mountPath: /etc/postgresql
          name: config-vol
      volumes:
      - name: config-vol
        configMap:
          name: db-config
```