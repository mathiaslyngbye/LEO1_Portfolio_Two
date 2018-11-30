# LEO1_Portfolio_Two
Repository containing a solution for the LEO1 portfolio assignment 2.


## Solution procedure:

### Enable bridged networking
In order to give containers persistant IP adresses, the following entries are added to */etc/lxc/dnsmasq.conf*.
* dhcp-host=lxcmail,10.0.3.100
* dhcp-host=ttrss,10.0.3.101

### Create containers
Two containers, C1 and C2, are created and launched through the following commands.
* lxc-create -n C1 -t download -- -d alpine -r 3.4 -a armhf
* lxc-create -n C1 -t download -- -d alpine -r 3.4 -a armhf
* lxc-start -n C1
* lxc-start -n C2

Running command *sudo lxc-ls -f* yields now the following output.

| NAME | STATE   | AUTOSTART | GROUPS | IPV4       | IPV6 |
|------|---------|-----------|--------|------------|------|
| C1   | RUNNING | 0         | -      | 10.0.3.171 | -    |
| C2   | RUNNING | 0         | -      | 10.0.3.195 | -    |
  

### Installing and starting lighttpd webserver in the first container
Container C1 is accessed through command *lxc-attach -n C1*. Within container C1, package list is updated and required packages are installed through the following commands.
* apk update
* apk add lighttpd php5 php5-cgi php5-curl php5-fpm

In file */etc/lighttpd/lighttpd.conf*, the following line is uncommented.
* include "mod_fastcgi.conf"

The lighttpd service is started thorugh the following command.
* rc-update add lighttpd default
* openrc

In folder */var/www/localhost/htdocs/*, file *index.php* (included in repository) is configured.


### Route host port to a container
In order to make the container C1 publicly accessible, the following command is executed (10.0.3.171 being the IP adress of container C1).
* iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 80 -j DNAT --to-destination 10.0.3.171:80


