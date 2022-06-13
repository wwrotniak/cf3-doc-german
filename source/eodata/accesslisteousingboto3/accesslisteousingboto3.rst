How to access/list EODATA using boto3?
=======================================

.. warning::

   We strongly recommend using virtualenv for isolating python packages. Configuration tutorial is presented below: `How to install Python virtualenv/virtualenvwrapper <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/pythonvirtualenv/pythonvirtualenv.html>`_


If virtualenv is activated:

.. code::

   (myvenv) eouser@vm01:~$ pip3 install boto3

Or if we install package globally:

.. code::

   eouser@vm01:~$ sudo pip3 install boto3

Two examples for listing products:

**Client**

 * low-level service access

 * generated from service description

 * exposes botocore client to the developer

 * typically maps 1:1 with the service API

 * snake-cased method names (e.g. ListBuckets API => list_buckets method)

.. code::

	  import boto3

	  access_key='YOUR_ACCESS_KEY'
	  secret_key='YOUR_SECRET_KEY'

	  host='http://data.cloudferro.com'

	  s3=boto3.client('s3',aws_access_key_id=access_key,
	  aws_secret_access_key=secret_key, endpoint_url=host,)

	  for i in s3.list_objects(Delimiter='/', Bucket="DIAS", Prefix='Landsat-8/OLI/L1TP/2020/11/09/',MaxKeys=30000)['CommonPrefixes']:
			  print(i)

**Resource:**

 * higher-level, object-oriented API

 * generated from resource description

 * uses identifiers and attributes

 * has actions (operations on resources)

 * exposes subresources and collections

.. code::
                                           
	  import boto3

	  access_key='16054e693d864fcc99f3345b9bac1881'
	  secret_key='d76bef9a48864fa885d0ea68671a166b'

	  host='http://data.cloudferro.com'


	  s3  = boto3.resource('s3',aws_access_key_id=access_key,aws_secret_access_key=secret_key, endpoint_url=host,)
	  bucket = s3.Bucket('DIAS')

	  # list all files in /eodata
	  for bucket_object in bucket.objects.all():
		 print(bucket_object.key)
	  #list all Sentinel-2 folders and products
	  for bucket_object in bucket.objects.filter(Prefix='Sentinel-2'):
		 print(bucket_object.key)
	 
 
Save your file with .py extension and run with the 'python3 <filename.py>' command in your terminal. For example:

.. code::

	  (boto3) eouser@vm01:~$ python3 boto_list.py



