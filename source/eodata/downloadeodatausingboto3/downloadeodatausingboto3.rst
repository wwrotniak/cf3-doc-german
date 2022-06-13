How to download EODATA file using boto3?
========================================

Download particular Landsat-5 image.

.. warning::

   We strongly recommend using virtualenv for isolating python packages. Configuration tutorial is presented below: `How to install Python virtualenv/virtualenvwrapper <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/pythonvirtualenv/pythonvirtualenv.html>`_

If virtualenv is activated:

.. code::

 (myvenv) eouser@vm01:~$ pip3 install boto3

Or if we install package globally:

.. code::

	 eouser@vm01:~$ sudo pip3 install boto3

**Script for downloading one .png file**

Remember to generate EC2 credentials for your project, as described here:  `How to generate EC2 credentials <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/generateec2/generateec2.html>`_
Remember that you cannot change the output file extension. In the other case the file content would be empty.

.. code::

	  import boto3
 
	  access_key='YOUR ACCESS KEY'
	  secret_key='YOUR SECRET KEY'
	  key='Landsat-5/TM/L1T/2011/11/16/LS05_RMPS_TM__GTC_1P_20111116T100042_20111116T100111_147386_0194_0035_4BF1/LS05_RMPS_TM__GTC_1P_20111116T100042_20111116T100111_147386_0194_0035_4BF1.BP.PNG'
	  host='http://data.cloudferro.com'
 
	  s3=boto3.resource('s3',aws_access_key_id=access_key,
	  aws_secret_access_key=secret_key, endpoint_url=host,)
 
	  bucket=s3.Bucket('DIAS')
 
	  bucket.download_file(key, '/home/eouser/image.png')

Save your file with .py extension and run with the 'python3 <filename.py>' command in your terminal. For example:

.. code::

	  (boto3) eouser@vm01:~$ python3 eodownload.py 

And here's result:

.. code::

	  (boto3) eouser@vm01:~$ python3 eodownload.py 
 
	  (boto3) eouser@vm01:~$ ls
 
	  eodownload.py  image.png
