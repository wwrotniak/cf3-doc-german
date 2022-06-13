How to download EODATA files using s3cmd?
=========================================

**Establishing connection**

At first, please verify your connection with EODATA bucket by using list command.

.. code..

   eouser@vm01:~$ s3cmd ls

You should obtain this output.

.. code..a

   2017-11-15 10:40  s3://DIASac
   2017-11-15 10:40  s3://EOCLOUD
   2017-11-15 10:40  s3://HRSI

If you have encountered any problems, please check all steps from this tutorial.
`How to access EODATA and Object storage using s3cmd? <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/datavolume/accessusings3cmd/accessusings3cmd.html>`_

**Downloading EOData product**

Entire product is being structured in a whole directory, not a single file. Therefore, you have to use **–recursive** parameter in order to avoid any “skipping” of files.
Example for downloading a Sentinel-2 product:

.. code..

   s3cmd get --recursive s3://EODATA/Sentinel-2/MSI/L2A/2022/01/30/S2B_MSIL2A_20220130T115209_N0400_R123_T28SFB_20220130T125446.SAFE/

The above command will download *S2B_MSIL2A_20220130T115209_N0400_R123_T28SFB_20220130T125446.SAFE* product to your local folder from which you are issuing the command.

Files can be also redirected to specific local folder. For our purposes it would be a *downloads* directory. Join path to local folder at the end of command.

.. code..

   eouser@vm01:~$ mkdir downloads
   eouser@vm01:~$ s3cmd -d get --recursive s3://EODATA/Sentinel-2/MSI/L2A/2022/01/30/S2B_MSIL2A_20220130T115209_N0400_R123_T28SFB_20220130T125446.SAFE/ downloads/

**Troubleshooting**

If nothing happens or you could not download a product properly, please issue **-d** switch to see a debug output for further diagnosis:

.. code..

  s3cmd -d get --recursive s3://EODATA/Sentinel-2/MSI/L2A/2022/01/30/S2B_MSIL2A_20220130T115209_N0400_R123_T28SFB_20220130T125446.SAFE/

**Alternative solution**

For syncing you are able to use **s3cmd sync** command (for the first time it downloads a whole product).

We can find a description in manual page (man s3cmd):

.. code..

   s3cmd sync LOCAL_DIR s3://BUCKET[/PREFIX] or  s3://BUCKET[/PREFIX]  LOCAL_DIR
   Synchronize a directory tree to S3 (checks files freshness using size and md5 checksum, unless overridden by options, see below)

Firstly we can create a new directory for our product and download product with **sync** command to this directory.

.. code..

   eouser@vm01:~$ mkdir example-product
   eouser@vm01:~$ s3cmd sync s3://EODATA/Sentinel-1/SAR/SLC/2018/10/01/S1B_WV_SLC__1SSV_20181001T234306_20181001T235605_012965_017F28_7E23.SAFE/ example-product/

Now we will present **sync** method in practice.

Move to your target directory and show files.

.. code..

   eouser@vm01:~$ cd example-product/
   eouser@vm01:~/example-product$ ls
   S1B_WV_SLC__1SSV_20181001T234306_20181001T235605_012965_017F28_7E23.SAFE-report-20181002T024920.pdf
   annotation
   manifest.safe
   measurement
   preview
   support

For our purposes we will **remove** a 'measurement' directory.

.. code..

   eouser@vm01:~/example-product$ rm -rf measurement/
   eouser@vm01:~/example-product$ ls
   S1B_WV_SLC__1SSV_20181001T234306_20181001T235605_012965_017F28_7E23.SAFE-report-20181002T024920.pdf
   annotation
   manifest.safe
   preview
   support

In order to sync data to local folder, you have to put a dot (**.** → location of the current directory) as a last sign.

.. code..
  
   eouser@vm01:~$ s3cmd sync s3://EODATA/Sentinel-1/SAR/SLC/2018/10/01/S1B_WV_SLC__1SSV_20181001T234306_20181001T235605_012965_017F28_7E23.SAFE/ ./

After invoke **s3cmd sync** command all missing files will be found and restored, as presented below.

.. code..

   Done. Downloaded 5347560568 bytes in 23.7 seconds, 214.86 MB/s.
   eouser@vm01:~/example-product$ ls
   S1B_WV_SLC__1SSV_20181001T234306_20181001T235605_012965_017F28_7E23.SAFE-report-20181002T024920.pdf
   annotation
   manifest.safe
   measurement
   preview
   support


