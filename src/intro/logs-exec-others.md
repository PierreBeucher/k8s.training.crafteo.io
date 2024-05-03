# Logs, exec and other basic operations

Lots of `kubectl` commands are direct equivalent of their `docker` / `podman` counterpart.

- Show logs for one of your running Pod
  - Equivalent of `docker logs`
  - You can also target a Deployment or Service
- Run a `sh`ell session in a Pod's container
  - Equivalent of `docker exec -it [container] sh`
  - Try to reach a Pod via it's Service DNS record (eg. `curl <service>.<namespace>.svc.cluster.local`)
- Get Deployment as YAML
  - Use an option of `kubectl get`
- Describe a Deployment
  - Equivalent of `docker inspect`