# StatefulSets

Deploy a Postgres database as StatefulSet by running command:

```
helm install my-postgres oci://registry-1.docker.io/bitnamicharts/postgresql -f resources/postgres-sts-values.yml
```

This command created a a few StatefulSets. _Note: Helm is a package manager for Kubernetes, an equivalent of `apt` or `yum` for Linux. We'll come back to Helm later._

- Use `kubectl` to describe Pods and PersistentVolumes. Observe the naming of pods.
- Try to delete a Pod and observe result.
- Delete Postgres Helm chart release with `helm delete my-postgres`. What happened to volumes?