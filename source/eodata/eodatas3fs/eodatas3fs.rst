How to mount eodata using S3FS (Linux)
======================================

EO DATA resources might be mounted to VM through s3 interface using s3fs command.

.. attention::
  Your virtual machine has to be launched in project with EO DATA!

1. Perform operation as a root

::

  # Perform all commands as root
  sudo -i

.. attention::
  Steps 2, 3 and 4 have already been made for each new VM images.

2. Install build and runtime dependencies for S3FS

::

  For  Ubuntu/Debian

  # Install git
  apt-get update
  apt-get --yes install git
  # Install required tools and libraries
  apt-get --yes install automake autotools-dev fuse g++ git libcurl4-openssl-dev libfuse-dev libssl-dev libxml2-dev make pkg-config

  For CentOS/RedHAT

  yum update
  yum install git
  yum install automake fuse fuse-devel gcc-c++ git libcurl-devel libxml2-devel make openssl-devel

3. Build s3fs

::

  git clone https://github.com/CloudFerro/s3fs-fuse.git
  cd s3fs-fuse/
  ./autogen.sh
  ./configure
  make
  # Install s3fs
  make install
  
4. Mount /eodata using s3fs

::

  # Prepare configuration for EO Data
  echo ACCESS:DATA >  ~/.passwd-s3fs
  chmod 600 ~/.passwd-s3fs

  # Comment out original fstab entry that mounted /eodata over NFS
  sed -i 's/nfs.eodata/#nfs.eodata/g' /etc/fstab

  # Add new entry to mount /eodata over s3fs
  echo s3fs#DIAS /eodata fuse passwd_file=/root/.passwd-s3fs,_netdev,allow_other,use_path_request_style,uid=0,umask=0222,mp_umask=0222,gid=0,url=http://data.cloudferro.com/ 0 0 >> /etc/fstab

  # Modify /etc/updatedb.conf to exclude s3fs mounts from indexing
  sed -i 's/PRUNEPATHS="/\PRUNEPATHS="\/eodata /g; s/PRUNEFS="/PRUNEFS="s3fs /g' /etc/updatedb.conf

5. Mount /eodata using s3fs

::

  # Remount /eodata
  umount -lf /eodata
  mount /eodata

The whole mount process on new VMs is automatic so if you don't want it to be done automatically, just remove the option noauto form /etc/fstab file.

::

  s3fs#DIAS   /eodata fuse    noauto,_netdev,allow_other,use_path_request_style,uid=0,umask=0222,mp_umask=0222,mp_umask=0222,gid=0,url=http://data.cloudferro.com,use_cache=1,max_stat_cache_size=60000,list_object_max_keys=10000,comment=cloudconfig    0   0

