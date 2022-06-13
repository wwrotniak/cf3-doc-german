How to mount Eodata using S3 protocol (Linux)?
==============================================

To provide access to EO Data repository each standard Linux based Virtual Machine image available in CloudFerro cloud has preinstalled filesystem emulation software s3fs. This is a stable and reliable solution, however due to its design, the access performance in terms of throughput is lower than direct s3 access using s3cmd or development libraries like boto.

Therefore for users who need filesystem access with higher throughput we prepared another solution based on tool called goofys.

It is designed to be very fast, however it does not provide full s3 compatibility and is less stable than s3fs. We have thoroughly tested all recommended tools and applications, and discovered that in some rare situations under heavy load goofys can hang and remounting of the repository might be required.

.. attention::
  Your virtual machine has to be launched in project with EO DATA!

To mount EO DATA using goofys filesystem emulation do following steps (this configuration was tested on Ubuntu 16 LTS):

Install git:

::

  $ sudo apt install git

Install goophys:

::

  $ sudo add-apt-repository ppa:gophers/archive && sudo apt-get update && sudo apt-get install golang-1.10-go
  $ echo "export PATH=\$PATH:/usr/lib/go-1.10/bin" >> ~/.profile
  $ source ~/.profile
  $ sudo -i
  # export GOPATH=/opt/go && go get github.com/kahing/goofys && go install github.com/kahing/goofys

  Exit sudo via Ctrl+d or "exit"

The configuration file in $HOME/.aws/credentials should have following content:

::

  [default]
  aws_access_key_id = accesseodata
  aws_secret_access_key = accesseodata

To mount the filesystem run this command:

::

  $ sudo $GOPATH/bin/goofys --endpoint http://data.cloudferro.com EODATA /eodata

In example above, CREODIAS is the name of the container (bucket), and /eodata is a sample mount point.
To automate this process you can remove or comment existing nfs mount point from fstab:

::

  nfs.eodata.cloudferro.com:/eodata/repository /eodata nfs ro,noauto,_netdev 0 0

and add following line:

::

  /opt/go/bin/goofys#EODATA /eodata fuse _netdev,allow_other,--endpoint=http://data.cloudferro.com,--file-mode=0666 0 0
