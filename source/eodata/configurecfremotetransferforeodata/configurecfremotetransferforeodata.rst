How to configure "CloudFerro Remote Transfer for EODATA" using s3cmd (Linux)?
==============================================================================

**Prerequirements**

    An active Creodias account is required. If you don't have an account, read the article `How to register to Portal? <https://creodias.eu/-/a-9-38>`_
    "CloudFerro Remote Transfer for EODATA" credentials must be created in advance.

    s3cmd must be installed. If you don't have installed, read the article `How to access EO DATA and Object Storage using s3cmd (Linux)? <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/datavolume/accessusings3cmd/accessusings3cmd.html>`_


In the solution we will use the following terms to describe:

**<ACCESS_KEY>** - your access key created on "https://clients.creodias.eu" website.

**<SECRET_KEY>** - your secret key created on "https://clients.creodias.eu" website.
 
**Configure s3cmd to use "CloudFerro Remote Transfer for EODATA"**


1. Type the command to configure s3cmd.

    
.. code::

   $ s3cmd --configure
   
2. Complete the configuration as below. **<ACCESS_KEY>** and **<SECRET_KEY>** are your credentials for "CloudFerro Remote Transfer for EODATA".

.. code::
   
   Enter new values or accept defaults in brackets with Enter.
   Refer to user manual for detailed description of all options.

   Access Key: <ACCESS_KEY>
   Secret Key: <SECRET_KEY>
   Default Region [US]:

   Use "s3.amazonaws.com" for S3 Endpoint and not modify it to the target Amazon S3.
   S3 Endpoint [s3.amazonaws.com]: s3.cloudferro.com

   Use "%(bucket)s.s3.amazonaws.com" to the target Amazon S3. "%(bucket)s" and "%(location)s" vars can be used if the target S3 system supports dns based buckets.
   DNS-style bucket+hostname:port template for accessing a bucket [%(bucket)s.s3.amazonaws.com]: s3.cloudferro.com

   Encryption password is used to protect your files from reading
   by unauthorized persons while in transfer to S3
   Encryption password:
   Path to GPG program [/usr/bin/gpg]:

   When using secure HTTPS protocol all communication with Amazon S3 servers is protected from 3rd party eavesdropping. This method is slower than plain HTTP, and can only be proxied with Python 2.7 or newer. 

   Use HTTPS protocol [Yes]: yes

   On some networks all internet access must go through a HTTP proxy.
   Try setting it here if you can't connect to S3 directly
   HTTP Proxy server name:

   New settings:
   Access Key: <ACCESS_KEY>
   Secret Key: <SECRET_KEY>
   Default Region: US
   S3 Endpoint: s3.cloudferro.com
   DNS-style bucket+hostname:port template for accessing a bucket: s3.cloudferro.com
   Encryption password:
   Path to GPG program: /usr/bin/gpg
   Use HTTPS protocol: True
   HTTP Proxy server name:
   HTTP Proxy server port: 0

   Test access with supplied credentials? [Y/n] y
   Please wait, attempting to list all buckets...
   Success. Your access key and secret key worked fine :-)

   Now verifying that encryption works...
   Not configured. Never mind.

   Save settings? [y/N]  y
   Configuration saved to '/home/eouser/.s3cfg'
   
3.Now you can use s3cmd commands (additional information about s3cmd: http://s3tools.org/usage)

.. code::

	  $ s3cmd ls

	  2017-12-11 15:30  s3://DIAS
	  2017-12-11 15:30  s3://EOCLOUD
	  2017-12-11 15:30  s3://EODATA
