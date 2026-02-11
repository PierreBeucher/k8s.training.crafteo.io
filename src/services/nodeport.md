# NodePort

L'application Example Voting App propose plusieurs services pour accéder à chaque composant.

- Modifier les services `vote` et `result` pour utiliser le type de service `NodePort`:
  ```yaml
  spec:
    type: NodePort
    ports:
    - name: "result-service"
      port: 5001
      targetPort: 80
      # Attention aux conflits de ports !
      # Comme tout le monde est sur le même cluster,
      # chacun doit utiliser des ports différents.
      # Utiliser un port entre 31000 et 32500
      nodePort: 31001
  ```
- Accéder à Vote et Result via un navigateur web en utilisant l'adresse IP publique ou le nom d'hôte d'un Node.
  - Utiliser `kubectl get node` et `kubectl describe node <node-name>` pour identifier l'IP publique des Nodes
  - Même si le port Node est ouvert et à l'écoute, il faut aussi des règles réseau et firewall pour accepter le trafic entrant
- À quoi correspondent `port`, `targetPort` et `nodePort` ?