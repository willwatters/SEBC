# Kinit checks

## The kinit command I used to authenticate my test user

```
[root@ip-172-31-32-222 etc]# kinit willwatters/admin@PUNEETHA.COM
Password for willwatters/admin@PUNEETHA.COM:
```


## The output from a klist command listing my credentials and ticket lifetime

```
[root@ip-172-31-32-222 etc]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: willwatters/admin@PUNEETHA.COM

Valid starting       Expires              Service principal
10/18/2018 09:27:02  10/19/2018 09:27:02  krbtgt/PUNEETHA.COM@PUNEETHA.COM
  renew until 10/25/2018 09:27:02

[root@ip-172-31-32-222 etc]# klist -e -f
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: willwatters/admin@PUNEETHA.COM

Valid starting       Expires              Service principal
10/18/2018 09:27:02  10/19/2018 09:27:02  krbtgt/PUNEETHA.COM@PUNEETHA.COM
  renew until 10/25/2018 09:27:02, Flags: FRI
  Etype (skey, tkt): aes128-cts-hmac-sha1-96, aes128-cts-hmac-sha1-96
  ```
