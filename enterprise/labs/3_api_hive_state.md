# Curl statements that stop, start and check the current state of Hive service

Check the current status of Hive Service (before stopping):

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v14/clusters/willwatters/services/hive/'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "GOOD_HEALTH"
```


Stop Hive Service:

```
[root@ip-172-31-32-222 tmp]# curl -X POST -u willwatters:cloudera -w "\n" http://localhost:7180/api/v14/clusters/willwatters/services/hive/commands/stop
{
  "id" : 246,
  "name" : "Stop",
  "startTime" : "2018-10-17T11:46:20.850Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```


Confirm Hive service has stopped:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v14/clusters/willwatters/services/hive/'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STOPPED",
  "healthSummary" : "DISABLED",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "DISABLED",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "DISABLED",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "STOPPED"
```

Start Hive service:

```
[root@ip-172-31-32-222 tmp]# curl -X POST -u willwatters:cloudera -w "\n" http://localhost:7180/api/v14/clusters/willwatters/services/hive/commands/start
{
  "id" : 250,
  "name" : "Start",
  "startTime" : "2018-10-17T11:53:14.056Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
```

Check the status of Hive service (after starting):

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v14/clusters/willwatters/services/hive/'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://ip-172-31-32-222.eu-west-3.compute.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "GOOD_HEALTH"
```
