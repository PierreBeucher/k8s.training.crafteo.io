# Persistent Volume Claims

Persistent Volume Claims (PVC) is a request for storage. By creating a PVC, you inform the cluster that you need a storage space and cluster will try to fulfill it.

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
        env:
        # postgres requires directory where data are created to be empty
        # Using default /var/lib/postgresql/data would result in failure
        # as it contains a "lost.found" directory, preventing server to initialize
        # Use this trick to have data in a sub-directory of created volume
        - name: PGDATA
          value: "/var/lib/postgresql/data/pg"
          
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