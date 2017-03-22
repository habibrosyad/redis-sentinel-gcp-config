# redis-sentinel-config
This is a sample config of Redis (with Sentinel) deployed in GCP via Cloud Launcher. When you've got the instances, the first thing you realize is Sentinel doesn't work as what you expect. Using Cloud Launcher, by defaults, your Redis instances will run on no-authentication mode. This is a problem because you either need to set password using `requirepass` and `masterauth` on all instances or just turn off the `protected-mode`. For the purpose of keeping the Redis secure, this sample config will use the first approach which add a password for the Redis cluster.

This sample config will assume your Redis master name is `master`. Also you might need to edit the following:
* In slave-node's `redis_node.conf`, replace `master-node` in `slaveof master-node 6379` with valid dns of your Redis master instance.
* In `sentinel.conf`, replace `127.0.0.1` in `sentinel monitor master 127.0.0.1 6379 2` will valid IP of your Redis master instance.

Don't forget to run this once you've done configuring the Redis instances.
```
sudo update-rc.d redis-sentinel defaults
```
By defaults redis-sentinel is not added to the default runlevel, so it can't run automatically when you reboot the instance.

## To Do
Create a script so that you can avoid typing it manually on all instances.