How to delete large S3 bucket?
==============================

**Introduction**

Due to an *openstack-cli* limitation removing S3 buckets with more then 10 000 objects will fail when using the command:

.. code::

  openstack container delete --recursive <<bucket_name>>

The command will fail with an error:

.. code::

   Conflict (HTTP 409) (Request-ID: tx00000000000001bb5e8e5-006135c488-35bc5d520-dias_default) clean_up DeleteContainer: Conflict (HTTP 409) (Request-ID:)

**Recommended approach**

To delete large S3 bucket we can use **s3cmd**.
In order to acquire access to Object Storage buckets via s3cmd, first you have to generate your own EC2 credentials with `this tutorial <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/generateec2/generateec2.html>`_.

Configure s3cmd with command:

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

After this operation, you should be allowed to list and access your Object Storage.

List your buckets with command:

.. code::

   eouser@vm01:$ s3cmd ls
   2022-02-02 22:22  s3://large-bucket


Now you're able to delete your large bucket with command presented below, where **-r** means recursive removal.

.. code::

   s3cmd rb -r s3://large-bucket

All files inside your bucket and specified bucket will be removed.

.. code::

   WARNING: Bucket is not empty. Removing all the objects from it first. This may take some time...
   delete: 's3://large-bucket/example_file.jpg'
   delete: 's3://large-bucket/example_file.txt'
   delete: 's3://large-bucket/example_file.png'
   ...
   ...
   ...
   Bucket 's3://large-bucket/' removed

Large bucket has been successfully removed, and our list of buckets is now empty.

.. code::

   eouser@vm01:$ s3cmd ls
   eouser@vm01:$  
