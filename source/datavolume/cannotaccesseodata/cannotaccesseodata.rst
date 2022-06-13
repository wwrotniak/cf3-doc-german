After remounting eodata i have an Error: "LS: CANNOT ACCESS '/EODATA/SENTINEL-1': NO SUCH FILE OR DIRECTORY"
============================================================================================================

Due to a nature of NFS in relation to our large repository, this kind of problems may appear from time to time if the connection to NFS server is lost for whatever reason.
In order to recover from such problems it is recommended to remount 

:: 

  /eodata. 

If local NFS cache is not purged after the remount, one may need to drop caches:

::

  User@CREODIAS_machine:~$ sudo -i
  User@CREODIAS_machine:~$ sync; echo 3 > /proc/sys/vm/drop_caches 
