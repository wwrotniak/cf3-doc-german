How to use Object Storage?
==========================

.. warning::

   It is highly advisable to put not more than 1 Mil (1 000 000) objects into one bucket (container).
   More objects makes listing of the objects very inefficient.
   We suggest to create many buckets with small amount of objects instead of small amount of buckets with many objects.
   
Be sure that you are **signed in**.

Go to: https://horizon.cloudferro.com/auth/login/?next=/

Choose the project. In that case we have just one project available named **"test"**.

.. figure:: objectstorage1.png

Open the **"Object Store"** pane

.. figure:: objectstorage2.png

Choose **"Containers"**

.. figure:: objectstorage3.png

Click **"+ Container"** button

.. figure:: objectstorage4.png

.. figure:: objectstorage5.png

Give the container a name "eg. C-01"

.. figure:: objectstorage6.png

If you want to make the container available outside of your project, check **"Public"** checkbox and click **"Submit"** button

.. figure:: objectstorage7.png

.. figure:: objectstorage8.png

You can now enter the container by clicking on "C-01" button

.. figure:: objectstorage9.png


To upload the files to the container, click the **"Upload file"** button

.. figure:: objectstorage10.png

.. figure:: objectstorage11.png


You can use **"Browse"** button to choose the file you want to upload from your file system

.. figure:: objectstorage12.png

.. figure:: objectstorage13.png

.. figure:: objectstorage14.png


You can share the link to the uploaded object by clicking **"Link"**

.. figure:: objectstorage15.png

.. figure:: objectstorage16.png

A link similar to this will be created:

:samp:`https://s3.waw3-1.cloudferro.com/swift/v1/AUTH_f22a47c247fc4372a00a0d0d794fbb32/C-01/image-01.pnga`

.. note::

   Links come and go and it is quite probable that this link is no longer valid at the moment you are reading this article. It only serves as an example of what you might get within this procedure. 

Now anybody who knows the link can download the object

.. figure:: objectstorage17.png


You can add folders in the container and upload objects to the new folders

.. figure:: objectstorage18.png

.. figure:: objectstorage19.png

.. figure:: objectstorage20.png

.. figure:: objectstorage21.png


You can create subfolders as well

.. figure:: objectstorage22.png

.. figure:: objectstorage23.png

.. figure:: objectstorage24.png


You can add more objects on various levels

.. figure:: objectstorage25.png

.. figure:: objectstorage26.png




