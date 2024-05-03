# Our first Pod !

Use `kubectl` to create a Pod:

```sh
kubectl run mypod --image us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21 --port 8080
```

This will create a Pod in default namespace. It's like `docker run` for Kubernetes. 

To reach your Pod externally, use:

```sh
kubectl port-forward pod/mypod --address 0.0.0.0 8081:8080
```

Your Pod is now reachable on port 8081. Try to reach it locally or via browser:

```
curl localhost:8081
```

This is the equivalent of running Docker command:

```sh
docker run -d -p 8081:81 us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21
```

---

In reality, `kubectl run` is rarely used, except for debug purposes. Most of the time _YAML Manifests_ are used to **describe** Kubernetes objects.

Create a Pod using YAML manifest with:

```sh
kubectl apply -f intro/pod.yml
```

- Use `kubectl` to get all Pods 
- Use `kubectl` to port-forward pod created via `intro/pod.yml`
- Delete both Pods with `kubectl delete`.