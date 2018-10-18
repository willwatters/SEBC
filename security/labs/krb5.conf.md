# Integrating Kerberos with Cloudera Manager

## /etc/krb5.conf

```
[root@ip-172-31-32-222 etc]# cat /etc/krb5.conf
[libdefaults]
default_realm = PUNEETHA.COM
dns_lookup_kdc = false
dns_lookup_realm = false
ticket_lifetime = 86400
renew_lifetime = 604800
forwardable = true
default_tgs_enctypes = aes128-cts arcfour-hmac
default_tkt_enctypes = aes128-cts arcfour-hmac
permitted_enctypes = aes128-cts arcfour-hmac
udp_preference_limit = 1
kdc_timeout = 3000
[realms]
PUNEETHA.COM = {
kdc = ip-172-31-32-222.eu-west-3.compute.internal
admin_server = ip-172-31-32-222.eu-west-3.compute.internal
}
[domain_realm]
```
