# CM Upgrade (including Agents) from 5.13 to 5.14


## API output status before the CM upgrade

Report the latest available version of the API:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/version'
v18
```

Report the CM version:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v18/cm/version'
{
  "version" : "5.13.3",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20180328-1830",
  "gitHash" : "f90c58536c252d70a23bde6d94514d92a1f111d4",
  "snapshot" : false
}[root@ip-172-31-32-222 tmp]#

```

List all CM users:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v18/users'
{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  }, {
    "name" : "willwatters",
    "roles" : [ "ROLE_ADMIN" ]
  } ]
}
```

Report the database server in use by CM:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera 'http://localhost:7180/api/v18/cm/scmDbInfo'
{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```


## API output status before the CM upgrade

Report the latest available version of the API:

```
[root@ip-172-31-32-222 yum.repos.d]# curl -u willwatters:cloudera 'http://localhost:7180/api/version'
v19
```

Report the CM version:

```
[root@ip-172-31-32-222 yum.repos.d]# curl -u willwatters:cloudera 'http://localhost:7180/api/v19/cm/version'
{
  "version" : "5.14.4",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20180707-0445",
  "gitHash" : "0971e84bdceb60db9b96533f46451f40ed8cbdf9",
  "snapshot" : false
}
```

List all CM users:

```
[root@ip-172-31-32-222 yum.repos.d]# curl -u willwatters:cloudera 'http://localhost:7180/api/v19/users'
{
  "items" : [ {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  }, {
    "name" : "willwatters",
    "roles" : [ "ROLE_ADMIN" ]
  } ]
}
```

Report the database server in use by CM:

```
[root@ip-172-31-32-222 yum.repos.d]# curl -u willwatters:cloudera 'http://localhost:7180/api/v19/cm/scmDbInfo'
{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```
