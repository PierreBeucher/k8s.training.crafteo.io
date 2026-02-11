# LoadBalancer

Un service LoadBalancer va automatiquement provisionner un Load Balancer:
- dans le Provider Cloud correspondant à notre cluster si il est déployé dans le Cloud
- Directement via des configurations internes pour un cluster on-prem

Configurer un Service de type Load Balancer:

- Modifier le service Vote pour qu'il soit de type `LoadBalancer`
  - Optionnel: retirer `nodePort: xxx` de la définition du Service qui n'est plus nécéssaire
- Observer le changement de comportement du service
  - Utiliser `kubect get svc` ou `kubectl describe ...`pour observer le nouveau status
- Repasser le type à `ClusterIP` et observer la suppression du Cloud Load Balancer
  **- Bien faire cette étape car les Load Balancers coûtent $$$, merci :-)**