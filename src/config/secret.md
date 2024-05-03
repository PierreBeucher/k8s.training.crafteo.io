# Secret

Secrets are much like ConfigMaps, except they are (theoretically) encrypted in Control Plane. Their access / usage should be protected with proper authorization in cluster.

Secrets require their config to be Base64 encoded. Use a command to encode a string in Base64:

```
echo -n "mypassword" | base64
```

_Note: Base64 is NOT encryption. It should not be used to protect a secret. Base64 is used as secrets can contain binary data and their base64 representation can be used as plain strings._

# Environment variables

Use Secret `resources/config/secret-postgres-env.yml` to set environment variables in Deployment

# Files as Volumes

Use Secret `resources/config/secret-postgres-config.yml` to mount a custom Postgres configuration in container at `/etc/postgresql/postgresql.conf`

# Use plain string in secrets?

Find a way to use plain strings instead of base64 data in your Secret YAML manifest.