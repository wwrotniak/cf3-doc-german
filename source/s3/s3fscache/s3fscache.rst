S3FS Cache
==========

By default, S3FS Cache is enabled in CREODIAS preconfigured Linux images. To examine its directory location you might take a look at the configuration in /etc/fstab.

.. code::

  #s3fs#DIAS /eodata fuse passwd_file=/root/.passwd-s3fs,_netdev,allow_other,use_path_request_style,uid=0,umask=0222,mp_umask=0222,mp_umask=0222,gid=0,stat_cache_expire=20,url=http://data.cloudferro.com,use_cache=1,max_stat_cache_size=60000,list_object_max_keys=10000 0 0

Use_cache parameter points on the folder “1” (it is located at the beginning of Filesystem Hierarchy /).

From the manual pages:

.. code::

  -o use_cache (default="" which means disabled)
  local folder to use for local file cache.

Directory “1” is being filled up during processing or downloading products from EOData repository to your local storage directly.

If you encounter problems with displaying the folders and/or files inside "/eodata" (e.g. "no such file or directory") please empty the "/1" folder.

To avoid the situation when you cannot remount your resources because the cache directory is occupying a whole left space on the disk, you might try to set a parameter ensure_diskfree.

Common prompt messages when you cannot remount an /eodata:

.. code::

  clnt_create: RPC: Timed out
  s3fs: There is no enough disk space for used as cache(or temporary) directory by s3fs.

From s3 manual pages, you can find out about ensure_diskfree parameter.

.. code::

  -o ensure_diskfree(default 0)
	
sets MB to ensure disk free space. This option means the threshold of free space size on disk which is used for the cache file by s3fs. s3fs makes file for downloading, and uploading and caching files. If the disk free space is smaller than this value, s3fs do not use diskspace as possible in exchange for the performance.

