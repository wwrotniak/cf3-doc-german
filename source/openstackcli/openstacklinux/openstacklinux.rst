How to install OpenStackClient (Linux)?
=======================================

**OpenStackClient** is very useful tool to gain a powerful management of our projects in Command Line Interface. It implements new features and advantages: You can run the commands from the CLI, or include prepared scripts in Python to automate the functionality of your cloud storage. Moreover we could reach our OpenStack access on any computer if we inset credentials (username and password).

Eventually everyone may admit that generally OpenStackClient provides more opportunities to look into our compute facility deeply and much more precisely.


.. Attention::

   It is strongly recommended to use virtual environments which do not affect system variables globally. If something goes wrong, everything is happening in separated space.

FAQ covers installation of Openstack Client under Ubuntu 18.04 LTS and Python 3. This method works on Ubuntu 20.04 as well.

Installation under other distributions may be simillar.

Let's start with the apt update && apt upgrade commands. This will update our system packages to the latest version
 
.. code::

   sudo apt update && sudo apt upgrade

Now let's install python3 and create a new python enviroment called simply "openstack_cli":

.. code::

   sudo apt install python3-venv
   python3 -m venv openstack_cli
   source openstack_cli/bin/activate
 
Now upgrade Python Package Installer (pip) to the latest version using command below:

.. code::

   pip install --upgrade pip

Finally install python-openstackclient:

.. code::

   pip install python-openstackclient

After this, you should be able to run openstack command from consone, eg:

.. code::
   
   openstack --help


If everything seems to work, we might firmly move on to our Horizon Panel.

Log in to your account. 

.. figure:: openstacklinux1.png
   :align: center

Head straight to our email button in the upper-right-corner. Click on it.

.. figure:: openstacklinux2.png
   :align: center

Choose **OpenStack RC File**.

Save your RC file on your disk.

If you use some text editor like vim it should consist of many variables related to your domain account like it:

.. figure:: openstacklinux3.png
   :align: center

Change your **directory** to downloading destination and **execute** the configuration file. 

For example it will look like: cloud_xxxxx/test-openrc.sh

Time to run this **sh** file. The prompted message will ask you for your domain **password**. Type it in and press **enter**. If the password is correct then you've got access **granted**.

.. code::
   
   . cloud_xxxxx/test-openrc.sh
   
   Please enter your OpenStack Password for project test as user johndoe:
   
After that you can, say, check list of your servers by typing in console:

.. code::

   openstack server list
   

Output of this command should contain table with ID, Name, Status, Networks, Image and Flavor of your virtual machines.

I recommend you to check Openstack documentation which contains lists of available commands. There you may reconsider many scenarios linked with your management.
 
