How to create volume Snapshot and attach as Volume (Linux/Windows)?
===================================================================

To create snapshot of the Volume:

•    Click Volumes tab in Horizon and choose "Create Snapshot" from dropdown menu.

•    Unmap disk in Windows VM, then in  Horizon click on option "Manage Attachments" -> "Detach Volume"


It is possible to create snapshot of attached volume but if any data are writen on it while creating snapshot, it might result in corrupted volume.

•    Convert snapshot into Volume - "Volume Snapshots" -> "Create Volume".

•    Map new Volume in your Windows VM.


For Linux systems you may mount that newly created Volume and access the data, the filesystem is the same as on the original Volume.

For example, if the Volume has one partition and is attached as **/dev/vdc**, do 

.. code::

   sudo mkdir /my_snapshot1 && sudo mount /dev/vdc1 /my_snapshot1
