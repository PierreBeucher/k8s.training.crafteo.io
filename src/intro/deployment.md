# Deployment: manage multiple Pods

Deployment manages multiple Pods.

- Create a Deployment with `kubectl` from manifest `intro/deployment.yml`. 
  - Use `kubectl --help`, a search engine or IA if needed
  - Command looks like `kubectl apply ...`
- List existing Deployments with `kubectl get`
- Restart the Pod created by our Deployment
  - There's no `restart` command, find another way
- Update your Deployment to have 3 replicas of our Pod