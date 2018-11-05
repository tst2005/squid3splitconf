# Squid3 config file spliter

# v0.2.x

How to switch from a full one big configuration file to a splited approach.

```sh
(root)# cp -a /etc/squid3/squid.conf /etc/squid3/squid.conf.orig
(root)# mkdir /etc/squid3/new
(root)# ./bin/squid3splitconf /etc/squid3/squid.conf /etc/squid3/new/

(root)# md5sum /etc/squid3/squid.conf
(root)# cat /etc/squid3/new/conf-available/*.conf |md5sum
(root)# mv /etc/squid3/new/conf-available/ /etc/squid3/
(root)# mv /etc/squid3/new/conf-enabled/ /etc/squid3/
(root)# rmdir /etc/squid3/new

(root)# echo 'include /etc/squid3/conf-enabled/*.conf' > /etc/squid3/squid.conf
```

# v0.1.x

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

