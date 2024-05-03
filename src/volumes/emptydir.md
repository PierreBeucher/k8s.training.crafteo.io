# emptyDir volume

`emptyDir` can be used in various situation, such as sharing data between container of the same Pod. For example to create a backup of database with a `postgres` container and upload result to AWS S3 with `aws-cli` container:

A backup CronJob is present at `resources/volumes/cronjob.yml` but lacks Volume configs. Adapt template to:

- Declare an `emptyDir` volume (use `volumes:` in appropriate place)
- Mount the volume at `/backup` for both containers 
- Create the CronJob and trigger it (create a Job from the CronJob) with
  ```sh
  kubectl create job --from=cronjob/postgres-backup manual-backup
  ```
- Observe the result 