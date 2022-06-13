Can't ping VM
=============

If you have problems with access to your VM - ping is not responding. Try the following:


install arping:

in CentOS:

::

   sudo yum install arping

in Ubuntu:

::

   sudo apt install arping

 

check the name of the interface connected to private network:

::

   ifconfig

based on the response, find the number of  the interface of 192.168.x.x (eth<number> or ens<number>)

after that invoke the following commands:

in CentOS:

::
   
   sudo arping -U -c 2 -I eth<number> $(ip -4 a show dev eth<number> | sed -n 's/.*inet \([0-9\.]\+\).*/\1/p')


in Ubuntu:

::

   sudo arping -U -c 2 -I ens<number> $(ip -4 a show dev ens<number> | sed -n 's/.*inet \([0-9\.]\+\).*/\1/p')


Next ping your external ip address and check if it helped.

