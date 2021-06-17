# Periodic upload

## Upload on a timer

In certain cases, your data might change hourly and you might want to update your datastore. You can configure your crontab to do this automatically.

Here's an example that uploads a new version of a datastore every hour:

```bash
#write out current crontab
crontab -l > mycron

#run datastore upload every hour every day
echo "0 * * * * grid datastores create --source data/path --name dataset" >> mycron    

#install new cron file
crontab mycron
rm mycron
```

