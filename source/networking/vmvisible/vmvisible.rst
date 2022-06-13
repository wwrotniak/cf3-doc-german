How is my VM visible in the internet with no Floating IP attached?
==================================================================

This article is written for clarification how the instance without floating IP adress would act if we would like to search it from machines being outside the project.

**How to find out what IP address is attached to VM?**

In Linux you can easily see your IP by executing command:

::

   curl ifconfig.me

In Windows, the easiest way is visiting website that shows us our public and private IP address, for example: `whatismyipaddress.com/ <https://whatismyipaddress.com//>`_

 

**Is my VM visible from internet without floating IP assigned?**

If we don't associate Floating IP with VM, their address is not going to be routable from the internet. While attempting to gain IP address using above-mentioned techniques we will see only interface address of the router attached to private network (by default it's 192.168.0.1)
 

**Can I send data from my VM outside without floating IP?**

Even though, Virtual Machine is open for the internet. So if you want to ingress data sent from VM to your external server, you should allow receiving packets from 192.168.0.1 in your firewall configuration.

 

**Is my VM accessible from the outside without floating IP?**

If a VM needs to be accessible from the Internet, a floating IP address must be attached to the instance. For more information regarding assigning Floating IPs to the instance, please see: `How to Add/Remove Floating IP’s to your VM? <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/networking/addremovefip/addremovefip.html>`_
