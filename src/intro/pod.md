# Notre premier Pod !

Les Pods et la plupart des objets Kubernetes sont par crées dans un _Namespace_. Un Namespace est une sorte d'espace indépendant où notre Pod sera créé dans le cluster Kubernetes pour éviter les conflits avec d'autres objets :

```sh
kubectl create namespace <your_ns>
```

Ensuite, créez un Pod dans notre namespace (l'option `-n` spécifie le namespace à utiliser) :

```sh
kubectl -n <your_ns> run mypod --image us-docker.pkg.dev/google-samples/containers/gke/whereami:v1.2.21 --port 8080
```

C'est l'équivalent de `docker run` pour Kubernetes.

Pour accéder à votre Pod de l'extérieur, utilisez:

```sh
kubectl -n <your_ns> port-forward pod/mypod --address 0.0.0.0 8081:8080
```

- `port-forward` créé un tunnel réseau directement depuis la machine depuis laquelle `kubectl` est lancé vers le container dans le cluster Kubernetes. Un équivalent de `docker run -p 8081:80 [...]`. - `--address` permet de binder l'écoute du port sur toutes les adresses (`localhost`) est utilisé par defaut pour permettre une connection à distance sur votre machine de TP

Votre Pod est maintenant accessible sur le port 8081. Essayez d'y accéder localement ou via un navigateur :

```sh
curl YOU.training.crafteo.io:8081
```
---

En réalité, `kubectl run` est rarement utilisé, sauf pour le debug. La plupart du temps, on utilise des _manifests ou configurations YAML_ pour **décrire** les objets Kubernetes.

Créer un Pod en utilisant un manifest YAML avec 

```sh
kubectl -n <your_ns> apply -f intro/pod.yml
```

Maintenant, utiliser les commandes `kubectl` pour :

- Lister tous les Pods
- Faire un port-forward du pod créé via `intro/pod.yml`
- Supprimer les deux Pods avec `kubectl delete`

---

Par défaut, `kubectl` récupère les Pods (et autres objets) dans le namespace `default`. Vous pouvez changer ce comportement avec :

```sh
kubectl config set-context --current --namespace pierre
```