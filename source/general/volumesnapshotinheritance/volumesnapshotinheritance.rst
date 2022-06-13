Volume snapshot inheritance and its consequences
=================================================

Performing a volume snapshot is a common form of securing your data against loss.
There is nothing wrong with that, but you should remember what the consequences are.


To illustrate the situation, we will present it on an example:

We have created a "VA" volume.

.. figure:: vsnap1.png

|

Next we create a "SA" snapshot from the "VA" volume.

.. figure:: vsnap2.png

|

From the OpenStack dashboard we can create new volumes "VB" and "VC" based on previously created snapshot "SA".

.. figure:: vsnap3.png

|

At the moment we have two new volumes which are based on the "SA" snapshot. Suppose we no longer need the "VA" volume and we want to delete it.

.. figure:: vsnap4.png
   :align: center

|

Unfortunately, delete will not be possible directly because to delete a given volume, we have to delete its snapshots.

.. figure:: vsnap5.png
   :align: center

|

So we must first delete the snapshot "SA", then the volume "VA".

However, this also will not be possible due to the fact that the "SA" snapshot is the source for 2 volumes "VB" and "VC".

To delete a volume from which snapshots volumes were created, we must also delete all snapshots of this volume.

In conclusion, when creating new volumes from a snapshot, remember about inheritance. Snapshot "SA" is a parent for the volumes (children) "VB" and "VC" and if we want to delete the volume "VA" we have to do it from the youngest generation (VB and VC).

 

Another solution are Backups, which do not create such bonds as snapshots and may exist even after the volume from which the backup was created has been deleted.
