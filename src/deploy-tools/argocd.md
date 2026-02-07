# ArgoCD

[ArgoCD] est un outil GitOps: il permet de déployer du workload Kubernetes de façon déclarative directement depuis un repository Git. 

C'est un serveur déployé directement sur Kubernetes qui va observer votre repository Git et synchroniser les modifications qui y surviennent. 

Par exemple, cette resource `Application` permet de déployer le contenu du repository Git [Example Voting App](https://github.com/PierreBeucher/k8s-training-exercises) depuis la branche `master`:

```yaml
# Exemple disponible dans resources/argocd/app.yml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: example-voting-app
spec:

  # Projet ArgoCD dans lequel déployer l'app
  project: sandbox

  # Source depuis laquell ArgoCD synchronisera les changements
  # Avec un fichier de values Helm
  source:
    repoURL: https://github.com/PierreBeucher/k8s-training-exercises
    targetRevision: master
    path: resources/helm/example-voting-app
    helm:
      valueFiles:
        - ../values/dev.yml
    
  # Destination dans laquelle sera déployée l'application
  # Par défaut le cluster dans lequel ArgoCD est déployé
  destination:
    server: https://kubernetes.default.svc
    namespace: VOTRE_NAMESPACE

  # Options supplémentaires
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

Le cluster Kubernetes est déjà configuré avec un serveur ArgoCD qui prendra en compte une `Application`. 

Configurer la ressource `Application` pour provoquer le déploiement de Example Voting App dans votre par ArgoCD dans votre namespace. 