# CM Monitoring Lab


## What is ubertask optimization?
Uberstask optimization runs "sufficiently small" jobs sequentially within a single JVM.

It is a YARN feature disabled by default.

The following settings exist for it in YARN configuration:

Enable Ubertask Optimization:
mapreduce.job.ubertask.enable: (disabled by default)

Ubertask Maximum Maps:
mapreduce.job.ubertask.maxmaps: current value 9

Ubertask Maximum Reduces:
mapreduce.job.ubertask.maxreduces: current value 1

Ubertask Maximum Job Size:
mapreduce.job.ubertask.maxbytes: current value 0


## Where in CM is the Kerberos Security Realm value displayed?
Administration > Settings > Kerberos > Kerberos Security Realm.
The default value is HADOOP.COM


## Which CDH service(s) host a property for enabling Kerberos authentication
To get a list of all the CDH services hosting a property for enabling Kerberos authentication - search for "Kerberos Principal" in the main search feature

This is a list of CDH services that host a property for enabling Kerberos authentication:

Flume
HBase
HCatalog
Hive
HttpFS
Hue
Impala
Llama
Oozie
Solr
Spark
Sqoop
ZooKeeper


## How do you upgrade the CM agents?
The first step is to upgrade the cloudera manager Server by getting the applicable repo for the required version and dong a Yum install.  It is reecommended to backup the current config incase of issues during the upgrade.

Once the CM server is upgrade and restarted a CM wizard is presented to upgrade the cloudera manager agents and optionally the JDK.


## Give the tsquery statement used to chart Hue's CPU utilization
Select cpu_system_rate + cpu_user_rate where category=ROLE and serviceType = HUE

This can be found via Search -> tsquery -> Chart Builder -> Examples


## Name all the roles that make up the Hive service
Gateway
Hive Metastore Server
HiveServer2
WebHcat Server


## What steps must be completed before integrating Cloudera Manager with Kerberos
Install `openldap-clients` on the Cloudera Manager Server host. Install `krb5-workstation` `krb5-libs` on ALL hosts
Install `MIT KDC` or use the `Active Directory KDC`
Create Kerberos Principal for the Cloudera Manager Server
Configure the KDC to allow renewable tickets with non-zero ticket lifetimes. Active Directory KDC allows it by default
Start the Wizard for Kerberos Integration
