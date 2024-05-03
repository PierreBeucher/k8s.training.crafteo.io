# LoadBalancer

A LoadBalancer service will provision automatically a Cloud Load Balancer pointing to our Nodes.

- Update Vote service to make it of type `LoadBalancer`
  - You can remove `nodePort: xxx` from Service definition
- Observe change in service behavior
  - Use `kubectl describe|get -o yaml` to observe new status
- Change back type to `ClusterIP` and observe Cloud Load Balancer deletion
  - Make sure to do that because Load Balancers cost $$$, thanks :)