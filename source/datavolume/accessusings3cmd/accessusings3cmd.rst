How to access EODATA and Object Storage using s3cmd (Linux)?
=============================================================

How to access EO DATA using s3cmd (Linux)

.. attention::

   Your virtual machine has to be launched in project with EO DATA!

You can install the s3cmd using Python PIP or from Linux repository.

**Installation from system repository on Debian/Ubuntu systems:**

Check for updates:

.. code::

   $ sudo apt update

Installing from repository:

.. code::

   $ sudo apt install s3cmd
   
**Installation from Python repository (on most Linux distributions with python and pip preinstalled):**

Installing with PIP:

Check if you have PIP installed

.. code::

   $ pip

   The program 'pip' is currently not installed. To run 'pip' please ask your administrator to install the package 'python-pip'
   
If not installed (Ubuntu):

.. code::

   $ sudo apt install python-pip

   $ pip --version

   pip 8.1.1 from /usr/lib/python2.7/dist-packages (python 2.7)

   $ sudo pip install s3cmd
   
If you see the following:

.. code::

   Traceback (most recent call last):
   File "/usr/bin/pip", line 11, in <module>
   sys.exit(main())
   File "/usr/lib/python2.7/dist-packages/pip/init.py", line 215, in main
   locale.setlocale(locale.LC_ALL, '')
   File "/usr/lib/python2.7/locale.py", line 581, in setlocale
   return _setlocale(category, locale)
   locale.Error: unsupported locale setting
   
add the following line:
 
.. code::
 
    export LC_ALL=en_US.UTF-8
    
to the file:
 
.. code::
 
    ~/.profile
    
Now you can check the .profile:
 
.. code::
 
   $ cat ~/.profile
   export LC_ALL=en_US.UTF-8
   $ source ~/.profile
   $ s3cmd --version
   s3cmd version 2.0.1
   
Configure s3cmd

.. code::

   $ s3cmd --configure
   

Enter new values or accept defaults in brackets with Enter.
Refer to user manual for detailed description of all options.

Access key and Secret key are your identifiers for Amazon S3. Leave them empty for using the env variables.

.. code::

   Access Key [access]:<ENTER>
   Secret Key [access]:<ENTER>
   Default Region [RegionOne]: <ENTER>
   Use "s3.amazonaws.com" for S3 Endpoint and not modify it to the target Amazon S3.
   S3 Endpoint [data.cloudferro.com:] <ENTER>
   Use "%(bucket)s.s3.amazonaws.com" to the target Amazon S3. "%(bucket)s" and "%(location)s" vars can be used
   if the target S3 system supports dns based buckets.
   DNS-style bucket+hostname:port template for accessing a bucket [%(bucket)s.s3.amazonaws.com]:  <ENTER>
   Encryption password is used to protect your files from reading
   by unauthorized persons while in transfer to S3
   Encryption password: <ENTER>
   Path to GPG program [/usr/bin/gpg]: <ENTER>
   When using secure HTTPS protocol all communication with Amazon S3
   servers is protected from 3rd party eavesdropping. This method is
   slower than plain HTTP, and can only be proxied with Python 2.7 or newer
   Use HTTPS protocol [No]: <ENTER>
   On some networks all internet access must go through a HTTP proxy.
   Try setting it here if you can't connect to S3 directly
   HTTP Proxy server name: <ENTER>
   
   New settings:
   
      Access Key: access
      Secret Key: access
      Default Region: RegionOne
      S3 Endpoint: data.cloudferro.com
      DNS-style bucket+hostname:port template for accessing a bucket: %(bucket)s.s3.amazonaws.com
      Encryption password:
      Path to GPG program: /usr/bin/gpg
      Use HTTPS protocol: False
      HTTP Proxy server name: _____
      HTTP Proxy server port: 0
   
    Test access with supplied credentials? [Y/n] <ENTER>
    Please wait, attempting to list all buckets...
    Success. Your access key and secret key worked fine :-)
    Now verifying that encryption works...
    Not configured. Never mind.
   
    Save settings? [y/N]  y <ENTER>
    Configuration saved to '/home/eouser/.s3cfg'
    
Now you can use s3cmd commands (additional information about s3cmd: http://s3tools.org/usage)

.. code::

   $ s3cmd ls
   
   2017-12-11 15:30  s3://DIAS
   2017-12-11 15:30  s3://EOCLOUD
   2017-12-11 15:30  s3://EODATA
   
   $ s3cmd ls s3://EODATA/
   
                          DIR   s3://EODATA/Envisat/
                          DIR   s3://EODATA/Landsat-5/
                          DIR   s3://EODATA/Landsat-7/
                          DIR   s3://EODATA/Landsat-8/
                          DIR   s3://EODATA/Sentinel-1/
                          DIR   s3://EODATA/Sentinel-2/
                          DIR   s3://EODATA/Sentinel-3/
                          DIR   s3://EODATA/Sentinel-5P/
                          
In order to acquire access to Object Storage buckets via s3cmd, first you have to generate your own ec2 credentials with `this tutorial <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/generateec2/generateec2.html>`_. 

After creation of credentials please remove file .s3cfg in Home folder and then reconfigure s3cmd by entering:

.. code::

   s3cmd --configure
   
and following values:

.. code::

   New settings:
   Access Key: (your EC2 credentials)
   Secret Key: (your EC2 credentials)
   Default Region: none
   S3 Endpoint: s3.waw3-1.cloudferro.com
   DNS-style bucket+hostname:port template for accessing a bucket: s3.waw3-1.cloudferro.com
   Encryption password: (your password)
   Path to GPG program: /usr/bin/gpg
   Use HTTPS protocol: True
   HTTP Proxy server name:
   HTTP Proxy server port: 0

After this operation, you should be allowed to list and access your Object Storage.
