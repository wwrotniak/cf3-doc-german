How to move a data volume between VMs?
======================================

Volumes may be moved from one VM to another. In Horizon the volume must be detached from one and attached to another. Detaching is not possible, however, from a running machine, which must be stopped first. Appropriate system reconfiguration should also take place: on the old machine the entry in /etc/fstab must be removed or commented out by editing file using a command (be extremely careful while applying changes!):

::
  
   sudo -e /etc/fstab

and new machine must be configured as in „`How to attach a volumes” <https://cloudferro-cf3.readthedocs-hosted.com/en/latest/datavolume/attachvolumetovmlessthan2tb/attachvolumetovmlessthan2tb.html>`_
