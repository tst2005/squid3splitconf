# Squid3 config file spliter

How to switch from a full one big configuration file to a splited approach.

```sh
(root)# cp -a /etc/squid3/squid.conf /etc/squid3/squid.conf.orig
(root)# mkdir /etc/squid3/conf-available/
(root)# ./bin/squid3splitconf /etc/squid3/squid.conf /etc/squid3/conf-available/

(root)# mkdir /etc/squid3/conf-enabled
(root)# cd /etc/squid3/conf-enabled
(root)# for f in ../conf-available/*; do if grep '^[^#]\+' "$f" | grep -q ''; then echo "$f"; ln -s "$f"; fi; done

(root)# echo 'include /etc/squid3/conf-enabled/*.conf' > /etc/squid3/squid.conf
```


