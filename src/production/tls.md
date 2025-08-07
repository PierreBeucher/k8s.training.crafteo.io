# Ingress avec TLS (HTTPS)

`resources/https` contient une ressource Ingress configurée avec TLS (HTTPS) et un Certificate [Cert Manager](https://github.com/cert-manager/cert-manager).

Déployer cet Ingress et le Certificate avec Example Voting App
- Vérifier que Example Voting App est déployée
- Déployer les ressources dans `resources/https`. **Remplacer `<YOUR_NAME>` dans les YAML par votre nom.**
- Observer la création des ressources Ingress et Certificate
- Tester la fonctionnalité. L'Ingress doit être accessible de l'extérieur. 