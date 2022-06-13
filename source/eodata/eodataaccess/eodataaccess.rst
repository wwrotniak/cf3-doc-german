EODATA access - S3 or NFS?
==========================

**S3FS**

By default in instances started from Linux images **/eodata** is automatically mounted v after adding the 'eodata_cloud[xxxxxxx]' network to your VM.

The /eodata mount runs as a service and the status can be checked by executing the command:

.. code::

	  sudo systemctl status eodata.mount

and can be restarted in case of problems by executing:

.. code::

	  sudo umount -lf /eodata
	  sudo systemctl restart eodata.mount

**NFS** 

If you want to mount eodata in Linux using NFS, you should stop the S3FS eodata.mount service:

.. code::

	  sudo systemctl stop eodata.mount

Modify /etc/fstab and uncomment the line:

.. code::

	  nfs.eodata.cloudferro.com:/eodata/repository    /eodata nfs     ro,noauto,_netdev,comment=cloudconfig   0       0

Save /etc/fstab and invoke:

.. code::

	  sudo mount /eodata
