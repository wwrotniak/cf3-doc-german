How to mount object storage in Linux?
=====================================

First, check if you have s3cmd installed by typing s3cmd. If not install it according to instructions:

::

   Command 's3cmd' not found, but can be installed with:
   sudo apt install s3cmd

If you do not have OpenStack client installed yet to install it with (sudo apt install python3-openstackclient)

Then load your cloud credentials with the command:

::

   source ~/cloud_XXXXX\ project_with_eo-openrc.sh

Check your credentials:

::

   openstack ec2 credentials list

where Access token and Secret token will be used in s3fs configuration:

::

  echo Access_token:Secret_token > ~/.passwd-s3fs

Change permissions of the new created file

::

  chmod 600 .passwd-s3fs

Uncomment "user_allow_other" in fuse.conf file as root

::

  sudo nano /etc/fuse.conf

Now you are ready to mount your object storage to your Linux system.

::

  s3fs w-container-1 /local/mount/point -o passwd_file=~/.passwd-s3fs -o url=https://s3.waw2-1.cloudferro.com -o use_path_request_style -o umask=0002 -o allow_other

More information about s3 protocol can be found:

`HOW TO ACCESS EODATA AND OBJECT STORAGE USING S3CMD (LINUX)? <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/datavolume/accessusings3cmd/accessusings3cmd.html?highlight=how%20to%20access%20eo>`_. 

`HOW TO ACCESS PRIVATE OBJECT STORAGE USING S3CMD OR BOTO3? <https://creodias.eu/-/how-to-access-private-object-storage-using-s3cmd-or-boto3->`_. 

