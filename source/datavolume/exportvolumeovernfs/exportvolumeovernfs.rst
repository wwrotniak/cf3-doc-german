How to export a volume over NFS (outside of a project)?
========================================================

**Prerequisites**

2 ubuntu servers in various projects (not in a private network) having floating IPs assigned.

::

   Host: 64.225.128.1
   Client: 64.225.128.2

On both servers we will create directory /xdata, that will be shared

 

**On the host**

::

   eouser@host:~$ sudo apt-get update
   eouser@host:~$ sudo apt-get install nfs-kernel-server
   eouser@host:~$ sudo mkdir /xdata
   eouser@host:~$ sudo chown nobody:nogroup /xdata
   eouser@host:~$ sudo nano /etc/exports

add line:

::

   /xdata 64.225.128.2(rw,sync,no_subtree_check)

save file

start the server:

::

   eouser@host:~$ sudo systemctl restart nfs-kernel-server

for Ubuntu 14.04 start the server with this command:

::

   eouser@host:~$ sudo service nfs-kernel-server start

 

Now go to https://horizon.cloudferro.com/project/security_groups/

| Create new security group.
| Give it a name (eg. allow_nfs) and save by clicking "Create security group" button.
| Click "manage rules".
| Click "add rule"
| Choose:
| Rule: Custom TCP Rule
|
| Direction: Ingress
| Openport: Port
| Port: 2049
| Remote: CIDR
| CIDR: 64.225.128.2

Click "Add"

Go to https://horizon.cloudferro.com/project/instances/

From the drop-down menu on the right of the "Host" instance, choose "Edit Security Groups"

| Click on the "plus" sign on the "allow_nfs" group.
| This will move the group from "All Security Groups" to "Instance Security Groups".
| Click "Save".
|

**On the Client**

::

   eouser@client:~$ sudo apt-get update
   eouser@client:~$ sudo apt-get install nfs-common
   eouser@client:~$ sudo mkdir /xdata
   eouser@client:~$ sudo mount 64.225.128.1:/xdata /xdata

You can check if the directory is mounted:

::

   eouser@client:~$ df -h
