# Rancher RBAC : comprendre le mapping avec Kubernetes RBAC

Rancher gère les utilisateurs et les permissions via son propre système: ces permissions sont implémentées via du RBAC K8S natif (eg. Roles, RoleBindings, ClusterRoles, ClusterRoleBindings).

## Créer un utilisateur

- Accéder à l'interface Rancher à l'adresse https://rancher.k8s.crafteo.io
- Créer un nouvel utilisateur avec votre nom sans lui affecter aucun role
  - A la création, n'affecter que les droits User-Base. Il n'est pas possible de spécifier des droits spécifiques lors de la création.

## Attribuer des permissions sur un cluster

Attribuer à votre utilisateur un scope **read-only** sur votre cluster
- L'affectation de droits sur un cluster se fait sur les configurations du Cluster directement, pas dans les configs Users globales

## Attribuer des permissions sur un projet et namespace

Créer un Projet à votre nom et lui affecter un Namespace
- Cluster > Projects/Namespaces > Create
- Utiliser votre Namespace ou créer un nouveau Namespace

Dans les configurations globales, créer un role custom _Pod Read-Only VotrePenom_
- _Users & Auth > Role Templates_
- Créer un Role Template au niveau Project/Namespace
- Verbs: `get`, `list`
- Resource: `Pods`

Sur votre cluster, créer un Projet et y affecter votre Namespace:
- Aller sur les options du Cluster et créer votre Projet + Namespace (ou affecter un Namespace existant)
- Attribuer votre utilisateur au scope read-only custom créé plus haut

## Observer les ressources RBAC créées

Rancher crée automatiquement des ressources Kubernetes RBAC pour matérialiser les permissions. 

Tracer le (Cluster)Role et (Cluster)RoleBinding de votre utilisateur:

- Users & Auths > chercher le nom associé à votre Role Template (eg. `rt-abcde`) et votre utilisateur (eg. `u-wz123`)
- Trouver le Role ou ClusterRole correspondant au Role Template (eg. `kubectl get clusterrole`)
- Trouver le RoleBinding ou ClusterRoleBinding liant votre utilisateur à ce Role ou ClusterRole
  - Il est possible qu'un ClusterRole soit utilisé par un simple RoleBinding sur un namespace (et non ClusterRoleBinding)
- Faire le lien entre les ressources Rancher et K8S RBAC

Créer un 2e Namespace dans votre projet et observer le résultat sur les Roles et RoleBindings