# Service: accessing our Pods

Manage Services ith manifests and access a Pod via Service

- Create a Service with `kubectl` using manifest `intro/service.yml`
  - Reminder: `kubectl apply -f ...`
- Use `kubectl port-forward` to expose the service locally and test access
  - Port forwarding will _forward_ a local port yo tour Pod. Use `curl localhost:PORT` or equivalent. 
  - `kubectl port-forward --help` or checkout official doc
- How does a Service identify which Pods to serve ?
- Delete Pods, Deployment and Service with a single `kubectl` command
- Re-apply our Deployment, Service and Pod with a single command