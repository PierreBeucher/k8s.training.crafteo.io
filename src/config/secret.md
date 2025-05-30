# Secret

Secrets are much like ConfigMaps, except they are (theoretically) encrypted in Control Plane. Their access / usage should be protected with proper authorization in cluster.

Secrets require their config to be Base64 encoded. Use a command to encode a string in Base64:

```
echo -n "mypassword" | base64
```

_Note: Base64 is NOT encryption. It should not be used to protect a secret. Base64 is used as secrets can contain binary data and their base64 representation can be used as plain strings._

# Use plain string in secrets?

By default secret values must be base64 encoded, eg:

```yaml
data:
    # "secretPassword" in base 64
    password: c2VjcmV0UGFzc3dvcmQ=
```

Find a way to use plain strings instead of base64 data in your Secret YAML manifest.

# Environment variables from Secrets

Use Secret `resources/config/secret-postgres-env.yml` to set environment variables in Postgres Deployment

# Files from Secrets

Copy ConfigMap `resources/config/configmap-postgres-config.yml` and transform it into a Secret to mount a custom Postgres configuration in container at `/etc/postgresql/postgresql.conf`

