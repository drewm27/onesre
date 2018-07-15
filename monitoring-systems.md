# Monitoring Systems

I believe in this day and age that a few types of monitoring systems are needed in an organization for complete coverage.

The first essential type is a classic object oriented system which will be used to monitor hardware status, networking equipment and non-dynamic services. This type of monitoring system allows for relational objects to be used allowing for host and service dependency creation. This allows for maintenance downtime to be created in a modular and inherited manner, along with an easy to understand representation of the entire infrastructure and how pieces relate. Nearly all of this structure, dependencies and configuration can be automatically generated out of the [Configuration Management Database](configuration-management-database.html). I believe that Nagios fits best here, see explanation in “Monitoring System.”

External monitoring is also be needed to allow us to make sure that the infrastructure is functioning from a client’s perspective. I believe Pingdom or any substitute works very well for this. Classic monitoring systems being used from a remote location also work well.

Metrics based monitoring is also needed for grouping or time series based alerts which are difficult to do in dynamic scaling environment like AWS, GCP or Kubernetes, [Prometheus](https://prometheus.io/) or [Telegraph/Influx/Chronograf/Kapacitor](https://www.influxdata.com/time-series-platform/) both work well.

Although in the future, as Kubernetes takes over, the classic object oriented monitoring system will only be needed for the underlying hardware.

## Classic Monitoring System Selection

I must also admit, after using Zabbix and Nagios since 2004, I’m still hugely in favor of moving to Nagios for the classic object oriented monitoring system. Here’s the critical areas where Zabbix falls down:
1. Zabbix has no display page of transient errors or monitoring flapping detection. How would you ever be able to find or detect a flapping service? You could easily have a service up only 50% of the time and never know.
2. The entire interface is quite a mess, you can’t even view hosts by hostgroup to get a wide view of the overall state of things.
4. Zabbix’s API is horrible, you can’t do everything in it, leading you to have to hand configure things. You can also get out of sync with your configuration management database as tracking every cluster and host addition and deletion cannot be done in an automated fashion. In the past, I was able to autogenerate all my Nagios config right out of our configuration management database anytime a host or group changed and just reload Nagios, which took about a second.
5. Zabbix relies on an SQL database which is another point of failure. Nagios doesn’t have any database dependency, state is tracked in a text file. This also means it’s much easier to create a high availability failover Nagios to automatically start when the master fails.

## Monitoring Hardware

Making sure you have all your bases covered in hardware monitoring is critical to the health and uptime of your services. Here’s a few items you should make sure you’re monitoring:
1. Setting up monitoring with smartctl on each of your hard drives for failures which should look for “FAILING” in the when_failed field when the hardware automatically triggers an issue. Hard drives are the #1 most likely to fail piece of hardware.
2. Monitoring for all types of RAID that you’re running. Software raid can be monitored from /proc/mdstat and using a script that looks for an _ for missing disks works well. Hardware raid should also be monitored. Hard drives are the #1 most likely to fail piece of hardware.
3. Monitoring for fan failures, which can be done through ipmitool chassis status. Fans are the #2 most likely to fail piece of hardware.
4. Monitoring for power supply failures which can be tricky based on the hardware type. Some may expose themselves through ipmitool, others may not.

