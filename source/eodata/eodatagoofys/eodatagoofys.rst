How to mount eodata as a filesystem using Goofys (Linux)?
=========================================================

To mount EO DATA resources as file system do following steps:

For Ubuntu:

.. code::

   $ sudo add-apt-repository ppa:gophers/archive && sudo apt-get update && sudo apt-get install golang-1.10-go
   $ echo "export PATH=$PATH:/usr/lib/go-1.10/bin" >> ~/.profile
   $ source ~/.profile
   $ mkdir work
   $ export GOPATH=$HOME/work && go get github.com/kahing/goofys && go install github.com/kahing/goofys

For Centos:

.. code::

   $ sudo rpm --import https://mirror.go-repo.io/centos/RPM-GPG-KEY-GO-REPO
   $ curl -s https://mirror.go-repo.io/centos/go-repo.repo | tee /etc/yum.repos.d/go-repo.repo
   $ sudo yum install golang

Next, create file ~/.aws/credentials

.. code::

   $ mkdir ~/.aws/
   $ touch ~/.aws/credentials

Put the following content into **~/.aws/credentials** eg.1234:

.. code::

   [s3]
   aws_access_key_id=1234
   aws_secret_access_key=1234

Create the directory, which will be the mount point for EODATA, like this:

.. code::

   mkdir ~/eo

invoke the following command:

.. code::

   $ $GOPATH/bin/goofys --region RegionOne --profile s3 --endpoint http://data.cloudferro.com DIAS ~/eo

DIAS is the name of our bucket that contains of EO DATA resources.

Now you can access the EODATA:

.. code::

   $ ls eo

  CAMS CLMS Elevation-Tiles Jason-3 Landsat-7 Sentinel-1 Sentinel-3 jason-3 CEMS CMEMS Envisat Landsat-5 Landsat-8 Sentinel-2 Sentinel-5P

If you want to mount EODATA on startup, you should do the following:

.. code::

   sudo mkdir /root/.aws
   sudo cp ~/.aws/credentials /root/.aws/

and add the following line to /etc/fstab:

.. code::

  /home/eouser/work/bin/goofys#DIAS /home/eouser/eo fuse _netdev,allow_other,--dir-mode=0777,--file-mode=0666,--region=RegionOne,--profile=s3,--endpoint=http://data.cloudferro.com 0 0

please comment out other options in /etc/fstab:

.. code::

   #nfs.eodata.cloudferro.com:/eodata/repository  /eodata nfs  ro,noauto,_netdev,comment=cloudconfig  0   0

   #s3fs#DIAS  /eodata fuse  noauto,_netdev,allow_other,use_path_request_style,uid=0,umask=0222,mp_umask=0222,mp_umask=0222,gid=0,url=http://data.cloudferro.com,use_cache=1,max_stat_cache_size=60000,list_object_max_keys=10000,comment=cloudconfig  0  0
