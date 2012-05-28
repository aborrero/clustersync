clustersync
===========

Tool for replicating and syncing config files and other data between nodes of a cluster.

This software is lincesed under GPL.


UNDER DEVELOPMENT!

Clustersync contact every node you configure looking for changes in files, using Rsync.
If any file have changed, then it copies the changes locally.

You can use this tool in a cluster, running on all nodes, as a method for syncing configuration files.
In order to work smothly, get transparent SSH between nodes you want to sync.

The configuration is easy, with only a few directives:

/etc/default/clustersync
========================
START="yes"
If start or not. Values {yes|no}. This option is readed just by the init.d script.

INTERVAL="30"
Interval between file checking. Value in seconds. 
Possitive integer expected, default will be used if missing. Default: 30

NODE_LIST=""
Where to connect to compare files. If empty, will do nothing.
A space separated list of FQDNs, IPv4 or IPv6.
In this way: NODE_LIST="192.168.2.2 myserver.example.com yourserver fe00::1"
As you can sync this file itself, be free to declare all nodes including the one running
this daemon in each node's NODE_LIST list.

FILE_LIST="/etc/clustersync.conf"
The file with the filelist to be synced.

USE_MD5="no"
Values: {yes|no} Default: no
For determining the sync rsync can work checking the time&size of a file
or checking the MD5 sum. Using MD5 is slower but in clustersync works better
in a scenario with lot of nodes.

LOGLEVEL="info"
Loglevel, Values: {no|info|warning|error|debug1|debug2} Default: info



/etc/clustersync.conf
=====================
Type a file in each line that will be synced, for example:
[...]
/etc/clystersync.conf
/etc/default/clustersync
/etc/hosts
/etc/resolv.conf
/etc/iptables.conf
/var/www/index.html
/srv/export/hello.txt
[...]
