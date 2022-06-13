Ephemeral vs Persistent storage (option "Create New Volume")
============================================================


The storage concepts present in OpenStack are described in OpenStack documentation

 https://docs.openstack.org/arch-design/design-storage/design-storage-concepts.html

 **Ephemeral storage**

 if the Virtual Machine is created with the option
 "Create New Volume" - "No" https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/vmnewvolumeno/vmnewvolumeno.html
 the disks associated with VMs are ephemeral, meaning that they will disappear when a virtual machine is terminated.
 
 **Persistent storage**

 if the Virtual Machine is created with the option
 "Create New Volume" - "Yes" https://cloudferro-cf3.readthedocs-hosted.com/en/latest/general/vmnewvolumeyes/vmnewvolumeyes.html
 and

 "Delete Volume on Instance Delete" - "No"

 the disks associated with VMs are persistant, meaning that they do not disappear when a virtual machine is terminated.
