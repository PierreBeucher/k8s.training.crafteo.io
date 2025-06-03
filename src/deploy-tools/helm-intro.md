# Helm: package manager for Kubernetes

[Helm](https://helm.sh/) is a "package manager" for Kubernetes. It uses YAML templates to manage Kubernetes resources and can be shared other package format (Container, NPM, etc.)

You can find Helm charts on [Artifact Hub](https://artifacthub.io/) or any search engine.

Usage example:  

```sh
helm --help

# Before installing a chart, adding a Repository is often required
# Adding "bitnami" repository
helm repo add bitnami https://charts.bitnami.com/bitnami

# You can also search for a Helm chart
# Search for "redis" charts
helm search repo redis

# Install a Redis chart
# 'myredis' is the Release name (like a container name for an image)
# 'bitnami/redis' is the chart to install
helm install myredis bitnami/redis
```

Adding a repository is not always required, a recent update allow to specify directly an OCI registry such as:

```sh
helm install my-redis oci://registry-1.docker.io/bitnamicharts/redis
```

## Install a Wordpress chart

Find a Wordpress chart and install it. Try to reach it externally using a port-forward.
- Wordpress is a blogging system with a database. It provides a simple frontend we'll try to reach from the internet.  
- Look for a Wordpress chart using any method

Once done, uninstall Wordpress your Wordpress chart's release
