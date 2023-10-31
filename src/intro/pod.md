# Our first Pod !

Use `kubectl` to create a Pod:

```sh
kubectl run mypod --image us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21 --port 8080
```

This will create a Pod in default namespace. It's like `docker run` for Kubernetes. 

To reach your Pod externally, use:

```sh
kubectl port-forward pod/mypod 8080:8080
```

Your Pod is now reachable on port 8080.

---

In reality, `kubectl run` is rarely used. Most of the time _YAML Manifests_ are used to **describe** Kubernetes objects.

Create a Pod using YAML manifest with:

```sh
kubectl apply -f intro/pod.yml
```

Delete it with `kubectl delete`.