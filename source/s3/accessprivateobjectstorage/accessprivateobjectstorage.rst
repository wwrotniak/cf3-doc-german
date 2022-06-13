How to access private object storage using S3cmd or boto3?
==========================================================

**Introduction**

Private object storage (buckets within user's project) can be used in various ways.
For example, to access files located in object storage, buckets can be mounted and used as a file system using **s3fs**.
Other tools which can be used to achieve better performance are **S3cmd** (command line tool) and **boto3** (AWS SDK for Python). 

**S3cmd**

In order to acquire access to Object Storage buckets via S3cmd, first you have to generate your own EC2 credentials with `this tutorial <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/generateec2/generateec2.html>`_.
Once EC2 credentials are generated, ensure that your instance or local machine is equipped in S3cmd:

.. code::

    s3cmd -V


If no, S3cmd can be installed with:



    apt install s3cmd


Now S3cmd can be configured with command:

.. code::

	  s3cmd --configure


add and confirm following values:

.. code::


	  Access Key: (your EC2 Access Key)
	  Secret Key: (your EC2 Secret Key)
	  Default Region: none
	  S3 Endpoint: s3.waw3-1.cloudferro.com
	  DNS-style bucket+hostname:port template for accessing a bucket: s3.waw3-1.cloudferro.com
	  Encryption password: (your password)
	  Path to GPG program: /usr/bin/gpg
	  Use HTTPS protocol: yes
	  HTTP Proxy server name:
	  HTTP Proxy server port: 0
  
	  Test access with supplied credentials? [Y/n] y
	  Please wait, attempting to list all buckets...
	  Success. Your access key and secret key worked fine :-)

	  Now verifying that encryption works...
	  Not configured. Never mind.

	  Save settings? [y/N] y


Configuration file will be saved in your home directory as '.s3cfg'
After this operation, you should be allowed to list and access your Object Storage.

List your buckets with command:

.. code::

	  eouser@vm01:$ s3cmd ls
	  2022-02-02 22:22  s3://bucket


To see available commands for S3cmd, please invoke:

.. code::

	  s3cmd -h


**boto3**


.. warning::

   We strongly recommend using virtualenv for isolating python packages. Configuration tutorial is presented below: `How to install Python virtualenv/virtualenvwrapper <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/pythonvirtualenv/pythonvirtualenv.html>`_

If virtualenv is activated:

.. code::

	 (myvenv) eouser@vm01:~$ pip3 install boto3

Or if we install package globally:

.. code::

	 eouser@vm01:~$ sudo pip3 install boto3

**Simple script for accessing your private bucket:**

.. code::

	  import boto3

	  def boto3connection(access_key,secret_key,bucketname):
	  host='https://s3.waw3-1.cloudferro.com'
	  s3=boto3.resource('s3',aws_access_key_id=access_key,
	  aws_secret_access_key=secret_key, endpoint_url=host,)

	  bucket=s3.Bucket(bucketname)

	  for obj in bucket.objects.filter():
		  print('{0}:{1}'.format(bucket.name, obj.key))

	  #For Python3
	  x = input('Enter your access key:')
	  y = input('Enter your secret key:')
	  z = input('Enter your bucket name:')

	  boto3connection(x,y,z)


Save your file with .py extension and execute the following command in the terminal:

.. code::

	  python3 <filename.py>

Enter the access key, secret key and bucket name. If all information are valid, you should see output in the format <bucket_name>:<file_name>.

  
