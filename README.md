# Redis Sentinel sample config (for GCP) 
This is a sample config of Redis (with Sentinel) deployed in Google Cloud Platform (GCP) via Cloud Launcher. When you've got the instances running, the first thing you will realized is Sentinel doesn't work as what you expect it to be. Using Cloud Launcher, by defaults, your Redis instances will run on protected-mode with no auth and no bind address. This is a problem because you either need to set password using `requirepass` and `masterauth` on all instances or just turn off the `protected-mode`. For the purpose of keeping the Redis secure, this sample config will use the first approach which add a password for the Redis cluster.

This sample config will assume your Redis master name is `master`. Also you might need to edit the `sentinel.conf`, replace `127.0.0.1` in `sentinel monitor master 127.0.0.1 6379 2` will valid IP of your Redis master instance. In the deployed Redis, you don't need to change any of these because Cloud Launcher has set it up for you. You just need to add few lines in `redis.conf` and `sentinel.conf` which you can find here.

Don't forget to run this once you've done configuring the Redis instances.
```
sudo update-rc.d redis-sentinel defaults
```
By defaults redis-sentinel is not added to the default runlevel, so it can't run automatically when you reboot the instance.

## To do
It might be nice to create an automation script so that you can avoid typing it manually on all instances.