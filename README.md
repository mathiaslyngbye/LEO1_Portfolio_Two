# LEO1_Portfolio_Two
Repository containing a solution for the LEO1 portfolio assignment 2.


## Solution procedure:

### Enable bridged networking
In order to give the containers persistant IP adresses, we write the following entries to /etc/lxc/dnsmasq.conf.
* dhcp-host=lxcmail,10.0.3.100
* dhcp-host=ttrss,10.0.3.101
### Second part
