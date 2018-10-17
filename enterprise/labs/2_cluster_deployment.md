# Use the API

## Output of API request using curl

Command run from CM host:

```
[root@ip-172-31-32-222 tmp]# curl -u willwatters:cloudera http://localhost:7180/api/v2/cm/deployment
{
  "timestamp" : "2018-10-17T11:25:16.930Z",
  "clusters" : [ {
    "name" : "willwatters",
    "version" : "CDH5",
    "services" : [ {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3lavrma7jgu0l9ekri0mq698g"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "aaok1ih63xqq1duaoyxs4hdxq"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "arv9wfg5sv6d2etegwhvpjgeq"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "8"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "3"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1800"
          }, {
            "name" : "rm_io_weight",
            "value" : "900"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "3"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "1024"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "4247"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "X3fcAZdrkrVTnCGTyIHgaNLQCHo2CB"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "6ciwjnzpbacvsqokzbp8chg9g"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "etfzv5sgpmj8wxknqd5n4x9x3"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7xxumbwhqhh3di6y9r011q9vf"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "br4hcn2hl9wihss4nplgkwv3a"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "520iqock0kawvfrtcgp8c1b83"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "37"
          }, {
            "name" : "role_jceks_password",
            "value" : "8u7djjurbo2yw6q6iwh5xqq68"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "3220069990"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "200"
          }, {
            "name" : "rm_io_weight",
            "value" : "100"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/dfs/jn"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          }, {
            "name" : "namenode_java_heapsize",
            "value" : "2242904064"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          }, {
            "name" : "secondary_namenode_java_heapsize",
            "value" : "2242904064"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "prHUXOsWIYAirluAlEvg6Fv7JvNsls"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "QhUEGoFiegPekDGhyqWZ26mqzt1AQz"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "8A939orqJbSGWG20qDAp0FB3oPJ0CP"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bjr7gse1o9ltl0wj6yb4pquq1"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "b1fla6go8jwwusfucdd938ayi"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8vadza988dn9tk2e799c2m0nr"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9apy2w0jfmjwl7b42spimuk0r"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4qc8rbjdq2g2vll5m7b2x8h2v"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "azi4z3fpqucr5xt05fcozxjh3"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-36d1c9b6ed57aa56ba62e33cfc54b4f4",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "80o1zpx7gx4mkjm7ragj50750"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "eko1fuhz6dmd1rmva78fs236r"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "6tzfr1ry5jna2nyqezyqu486a"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-a6c23e442a5c8851ef1b67a0f6b3fe42",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "39"
          }, {
            "name" : "role_jceks_password",
            "value" : "cqfzf51lzgtjf1lhdagn4q9ip"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-ebccca0c0cb395d9f007e1c2b997a59c",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "45"
          }, {
            "name" : "role_jceks_password",
            "value" : "cjepdc15ucv8bcst9hogzk91n"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    }, {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "52428800"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "52428800"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "912680550"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "153"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-172-31-32-222.eu-west-3.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "password1"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "e90rrk8ir8h8s97tuomu4ectc"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-99f170146971fb5d59aa6b7bde3d9a78",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "es2nfg1s8vmn7nsmwhp5h5m35"
          } ]
        }
      } ],
      "displayName" : "Hive"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4",
    "ipAddress" : "172.31.32.222",
    "hostname" : "ip-172-31-32-222.eu-west-3.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "37e93833-b9f5-4869-8ac8-325d43aa34cd",
    "ipAddress" : "172.31.38.0",
    "hostname" : "ip-172-31-38-0.eu-west-3.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "4862bce2-ebdf-47c9-9493-7654b7f80088",
    "ipAddress" : "172.31.39.85",
    "hostname" : "ip-172-31-39-85.eu-west-3.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "23c7bee5-8bf3-4788-932e-89e0ce0be2bc",
    "ipAddress" : "172.31.46.203",
    "hostname" : "ip-172-31-46-203.eu-west-3.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "552aeed7-1b68-436c-b758-1aeb422628c8",
    "ipAddress" : "172.31.47.1",
    "hostname" : "ip-172-31-47-1.eu-west-3.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__mgmt-ACTIVITYMONITOR-18adb60503749c6995f3f5b7b8c53753",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "e143e52241468910d3ab29a5737da9200e5511cfb11910aa5261f040f34a99df",
    "pwSalt" : 4494154253958199994,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-18adb60503749c6995f3f5b7b8c53753",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "c54701d115db058bd2b421407fa79ef9527700f46167727b115bd86ea5c09558",
    "pwSalt" : -7975812546777232568,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-18adb60503749c6995f3f5b7b8c53753",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "d5583eaa3c0a0ed5aa77aa108c3afb757f9093948466a11b85aa631696b7c36f",
    "pwSalt" : -5540013925046635909,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-18adb60503749c6995f3f5b7b8c53753",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "6964b35e78d3bdd5ff9a2dcf773218f2d153fa2951c5aab692570c0284d1506c",
    "pwSalt" : 907429565862425799,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-18adb60503749c6995f3f5b7b8c53753",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "febfac93485904001d9c96071deeb04456854063fae8bb99b492969156304895",
    "pwSalt" : 6117054824415696275,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "62377c76002f2e8ed50ff949784f0dbf21295df999d3db9f45946e057141da13",
    "pwSalt" : -2304125917660211911,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "f83093d45081340ab9eea4837c10d073f2eb692faca775db672e8357181136fd",
    "pwSalt" : 7549521392275108615,
    "pwLogin" : true
  }, {
    "name" : "willwatters",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "2e808f7f078f5c0a8809e4df1c3a1b3369eb6bf9b29c85912e575b8aa4128ab7",
    "pwSalt" : 4749443805761627709,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.13.3",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20180328-1830",
    "gitHash" : "f90c58536c252d70a23bde6d94514d92a1f111d4",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "ACTIVITYMONITOR",
        "items" : [ {
          "name" : "firehose_database_host",
          "value" : "ip-172-31-32-222.eu-west-3.compute.internal"
        }, {
          "name" : "firehose_database_name",
          "value" : "amon"
        }, {
          "name" : "firehose_database_password",
          "value" : "password1"
        }, {
          "name" : "firehose_database_user",
          "value" : "amon"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-172-31-32-222.eu-west-3.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "password1"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ACTIVITYMONITOR-18adb60503749c6995f3f5b7b8c53753",
      "type" : "ACTIVITYMONITOR",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "8vf3eiyjpl320f59uzd9dqaj8"
        } ]
      }
    }, {
      "name" : "mgmt-ALERTPUBLISHER-18adb60503749c6995f3f5b7b8c53753",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "27618fmvlufmjeuixygcmmyae"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-18adb60503749c6995f3f5b7b8c53753",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "8di80s5ryb7qmd17yj1gr07be"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-18adb60503749c6995f3f5b7b8c53753",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "3wxbohc4mz46aonc3jzz96hd4"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-18adb60503749c6995f3f5b7b8c53753",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "57wx9b977po0p5itz34ebsfk8"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-18adb60503749c6995f3f5b7b8c53753",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "e5c63c02-36c0-4bad-9b1b-8286e27a3ea4"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "yfapm254lgsah00fy5uk9fau"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/25/2012 18:30"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "http://172.31.32.222/cdh/"
    } ]
  }
```
