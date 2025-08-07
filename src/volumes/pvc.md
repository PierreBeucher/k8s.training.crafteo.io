# Persistent Volume Claims

Un Persistent Volume Claim (PVC) est une demande d'espace de stockage. En créant un PVC, tu indiques au cluster que tu as besoin d'un espace de stockage et le cluster va essayer de le fournir.

- Créer un PVC à partir de `resources/volumes/pvc.yml`
- Mettre à jour le déploiement Database pour attacher le PVC créé:
```yml
apiVersion: apps/v1
kind: Deployment
# [...]
spec:
  template:
    spec:
      containers:
      - name: postgres
        # [...]
        env:
        # postgres requiert que le dossier où les données sont créées soit vide
        # Utiliser le chemin par défaut /var/lib/postgresql/data provoquerait une erreur
        # car il contient un dossier "lost.found", empêchant le serveur de s'initialiser
        # Utiliser cette astuce pour stocker les données dans un sous-dossier du volume créé
        - name: PGDATA
          value: "/var/lib/postgresql/data/pg"
          
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: db-data
      volumes:
      - name: db-data
        persistentVolumeClaim:
          claimName: db-data-pvc # Le nom doit correspondre au nom du PVC
```
- Trouver le Persistent Volume (PV) créé suite à ta demande de stockage via le PVC
- Détruire et recréer le déploiement Database, vérifier que le PVC est resté intact