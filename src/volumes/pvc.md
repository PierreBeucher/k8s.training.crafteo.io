# Persistent Volume Claims

Persistent Volume Claims (PVC) is a request for storage. By creating a PVC, you inform the cluster that you need a storage space and cluster will try to fullfill it.

- Create a PVC from `resources/volumes/pvc.yml`
- Update Database deployment to attach the PVC you created. Use something like:
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
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: db-data
      volumes:
      - name: db-data
        persistentVolumeClaim:
          claimName: db-data-pvc # Name must match PVC name
```
- Find the Persistent Volume (PV) created as per your request for storage via PVC 
- Destroy and recreate Database deployment, verify PVC remained intact