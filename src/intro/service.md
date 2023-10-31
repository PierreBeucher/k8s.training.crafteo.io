# Service: accessing our Pods

- Create a Service with `kubectl` using manifest `intro/service.yml`
- Use `kubectl port-forward` to expose the service locally and test access
- Observe which Pod is reached each time service is used
- How does a Service identify which Pods to serve ?
- Delete Pods, Deployment and Service with a single `kubectl` command