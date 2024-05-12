# Our first Pod !

Let's create our first Pod. 

Start by creating a _Namespace_. A Namespaces is like an independent place where our Pod will be created in Kubernetes cluster to avoid conflict with other objects:

```sh
kubectl create namespace <your_ns>
```

Then create a Pod in our namespace (`-n` flag specify namespace to use):

```sh
kubectl -n <your_ns> run mypod --image us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21 --port 8080
```

It's like `docker run` for Kubernetes. 

To reach your Pod externally, use:

```sh
kubectl -n <your_ns> port-forward pod/mypod --address 0.0.0.0 8081:8080
```

Your Pod is now reachable on port 8081. Try to reach it locally or via browser:

```sh
curl YOU.training.crafteo.io:8081
```

This is the equivalent running Docker command below, except our Pod (and container) are not reachable locally but only within the Kubernetes cluster. 

```sh
docker run -d -p 8081:81 us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21
```

---

In reality, `kubectl run` is rarely used, except for debug purposes. Most of the time _YAML Manifests_ are used to **describe** Kubernetes objects.

Create a Pod using YAML manifest with:

```sh
kubectl -n <your_ns> apply -f intro/pod.yml
```

Now, use `kubectl` commands to:

- Get all Pods 
- Port-forward pod created via `intro/pod.yml`
- Delete both Pods with `kubectl delete`

---

By default `kubectl` fetch Pods (and other objects) in the `default` namespace. You can change this behavior with:

```sh
kubectl config set-context --current --namespace pierre
```