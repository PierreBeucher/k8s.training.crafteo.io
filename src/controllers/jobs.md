# Jobs and CronJobs

Use a CronJob to vote every minute (yeah, that's cheating)

## Deploy CronJob

- Deploy CronJob `resources/cronjob.yml`
- Analyze CronJob template content. Why is `spec` specified multiple times?
- What's the CronJob schedule ?

## Parallelism

Update your CronJob to run 3 instances of Jobs every minute instead of 1. 

## Trigger Job manually on-demand

Run a `kubectl` command to trigger manually Job from CronJob without waiting for schedule time.