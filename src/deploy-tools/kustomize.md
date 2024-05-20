# Kustomize

Kustomize is a built-in `kubectl` tool for multi-environment and configuration management features. 

See [Kustomize Official documentation](https://kubectl.docs.kubernetes.io) and [reference documentation](https://kubectl.docs.kubernetes.io/references/kustomize/)

## Kustomize Example Voting App

Kustomized applications need:

- A _base_ with our YAML config (Deployment, Services, etc.) and a `kustomization.yml` listing desired resources along with some options.
- One or more overrides (typically per environment, but not necessarily)

To Kustomize Example Voting App:

- Copy `resources/kustomize/base-kustomization.yml` into `base/kustomization.yml`. This file references all Example Voting App resources.
- Use one of `resources/kustomize/dev` or `resources/kustomize/prod` with `kubectl`. Note that they each reference their base using a relative path, eg. `resources: [ "../../../base" ]`
  
```sh
#
# Mind the -k
#
# Like kubectl apply -f but will read from dev and all referenced resources (including base)
kubectl apply -n <YOU> -k resources/kustomize/dev
```

Observe result based on dev and base `kustomization.yml` files content, especially `commonLabels`

## Set namespace

Create a namespace using your name prefixed with `-kustomize`, eg. `YOU-kustomize`.

Update dev's `kustomization.yml` to set namespace `YOU-kustomize` and apply without `-n xxx` flag, eg:

```sh
kubectl apply -k resources/kustomize/dev
```

What happened to resources in previous namespace ?

## Patches and ConfigMap/Secret generators

Use a [ConfigMap generator](https://kubectl.docs.kubernetes.io/guides/config_management/secrets_configmaps/) to create a ConfigMap from file `postgresql.conf` file

Use a [Secret generator](https://kubectl.docs.kubernetes.io/guides/config_management/secrets_configmaps/) to create a Secret from file `postgres-secret.properties` file
- You'll need additional options to consider this file as environment variables

Override Deployment using a _patch_ to ensure Secret and ConfigMap values are used instead of values set in base.
- Use `db-deployment-patch.yml` and update `kustomization.yml`

## Adapt another Kustomization

Reproduce changes from `dev` Kustomization to `prod` Kustomization and deploy them both in the same namespace. 