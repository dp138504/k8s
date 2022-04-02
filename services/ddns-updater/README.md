# DDNS Updater

To install:
1) Edit `inadyn-cfgmap.yml` with the proper values.
2) `kubectl create ns ddns`
3) `kubectl apply -f . -n ddns`
4) Wait for the CronJob to kick off or manually trigger execution.
5) Ensure pod logs show successfull update.