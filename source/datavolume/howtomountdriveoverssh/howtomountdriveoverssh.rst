
How to mount Network Drive over SSH in Windows?
===============================================

**You can mount VM disk to your system using SSH.**

To do that you have to download and install following programs:

* `PuTTy <https://www.putty.org/>`_
* `Dokan <https://github.com/dokan-dev/dokany/releases>`_
* `WinFsp <https://github.com/billziss-gh/winfsp/releases/tag/v1.10>`_
* `SSHFS-Win and SSHFS-Win-Manager <https://github.com/billziss-gh/sshfs-win>`_ (to Authenticate using OpenSSH Key)

**Firsly you have to convert your Private Key to OpenSSH format.**

To do that please launch PuTTy KeyGenerator then choose your Private Key by going to *File* - *Load Private Key*

.. image::  puttymenu.png

Then Please export your Private Key by going to *Conversions* and then *Export OpenSSH key*.

.. image:: puttyopenssh.png

**After that you can close PuTTy and open SSHFS-Win-Manager**

.. image:: sshfsmenu.png

To add new connection simply click on *Add Connection*

.. image:: sshfsaddconn.png

Then you'll see window where you can specify all connection details.

Here's a short description of the options.

* **Name** - you can specify connection name
* **IP/HOST** - that's simply your VM floating IP
* **PORT** - default it's 22 (SSH port number)
* **USER** - specify user name to authenticate with
* **AUTHENTICATION METHOD** - you can choose two authentication methods, by password or using OpenSSH key
* **PATH** - set path to Directory that you want to mount
* **DRIVE LETTER** - you can choose on which letter the new drive will be named 

eg.

.. image:: sshfsconnectionfilled.png

Under **KEY FILE** option I choosed path to OpenSSH key file that has been exported before.

Then click save. You'll see that new connection has been made.

.. image:: sshfsconnection.png

Then just click link button. 

And your drive shoul be mounted.

.. image:: thispc.png
