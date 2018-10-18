# Integrating Kerberos with Cloudera Manager

## /var/kerberos/krb5kdc/kdc.conf (before Kerberos Enablement Wizard)

```
[root@ip-172-31-32-222 etc]# cat krb5.conf
# Configuration snippets may be placed in this directory as well
includedir /etc/krb5.conf.d/

[logging]
default = FILE:/var/log/krb5libs.log
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/kadmind.log

[libdefaults]
dns_lookup_realm = false
dns_lookup_kdc = false
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
default_realm = PUNEETHA.COM
default_ccache_name = KEYRING:persistent:%{uid}
udp_preference_limit = 1
default_tgs_enctypes = aes128-cts arcfour-hmac
default_tkt_enctypes = aes128-cts arcfour-hmac

[realms]
PUNEETHA.COM = {
  kdc = ip-172-31-32-222.eu-west-3.compute.internal
  admin_server = ip-172-31-32-222.eu-west-3.compute.internal
}

[domain_realm]
.example.com = PUNEETHA.COM
example.com = PUNEETHA.COM
