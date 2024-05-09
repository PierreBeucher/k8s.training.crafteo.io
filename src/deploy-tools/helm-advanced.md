# Helm advanced: writing a Helm charts

Directory `resources/helm/example-voting-app` contains a Helm chart with templated YAML manifests.

## Deployment, update and values

Use `helm install` command to deploy a release of the Example Voting App chart.
- Verify it works via port-forward
- Explore YAML templates to understand templating mechanisms and its connection to `values.yml`

You can override `values.ym`l with external configuration files, typically by environment.
- Update your release to override the default values using resources/helm/values/dev.yml

## Secrets Management

Helm doesn't provide a native mechanism for managing secrets. A common pattern is to reference an external secret (not managed by the chart).

Update your Helm release using `resources/helm/values/prod.yml` values.
- This configuration references an external secret, **you must create it on your own**
- Explore the contents of the chart to understand the underlying mechanism

There are also [Helm plugins](https://helm.sh/docs/topics/plugins/) that allow secret management such as [`helm-secrets`](https://github.com/jkroepke/helm-secrets)