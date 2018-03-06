.. _Edge_Install_topic:

How to Pull the Edge Data Server Docker Image
=============================================

The Edge Data Server Docker image is stored in the Azure Container Registry. Pulling the Edge Data Server Docker image
is relatively straightforward; however, the Azure CLI tools are required in order to log in. Instructions
for downloading the Azure CLI tools are available `here <https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest>`_ 

Generally, end users will not install the Azure CLI tools on their Internet of things (IOT) devices. An easy way
to install a minimal-footprint Docker image on an IOT device is to download the image to an intermediate
PC, export the image from the PC, copy the export to the device, and import the image to Docker on the device. The
intermediate PC can pull either the x64 or the ARM image; the architecture of the image is not required to match the
architecture of the PC as long as no attempt is made to run a mismatched image on the PC.

Logging In
----------

First, install the Azure CLI tools using the instructions on the Microsoft web site shown above. Next, log in to the
Container Registry using the following command:

::

  az acr login --name edgedev --username <username> --password <password>

The account provided to you is a read-only account that allows access to the Docker registry that stores the Edge
Data Server Docker images. After the command is run, you are authenticated to use the ``docker pull`` command to pull
the desired image to your local Docker installation. Because the Azure CLI takes over the login function, a 
``docker login`` command is not required.

Pulling the Image
-----------------

After the login has succeeded, all that is necessary is to pull the image from the remote registry using a
``docker pull`` command, as shown here:

::

  docker pull edgedev.azurecr.io/osisoft/edgedataserver: <tag>

The tag consists of the desired architecture (``x64`` or ``ARM``) and the build number, or "latest" for the latest build.
So to obtain the latest ARM build, use the following command:

::

  docker pull edgedev.azurecr.io/osisoft/edgedataserver:ARM-latest

To obtain the 20180101.1 build for the x64 architecture, use the following command:

::

  docker pull edgedev.azurecr.io/osisoft/edgedataserver:x64-20180101.1

Starting a Container
--------------------

After pulling the image, you can start a container that is based on the pulled image, as shown in the following command. 
The simplest startup scenario is where the port exposed by the server (5000) is not surfaced through the host; 
rather it is internal to the internal Docker network, and no host drive space is mapped into the container.

::

  docker run -itd edgedev.azurecr.io/osisoft/edgedataserver:x64-latest

To expose port 5000 through the host so that applications running on the host (or elsewhere on your local
network) can access the server, add ``-p 5000:5000`` to the command line before the image name.

To map a local folder into the container (such as when you want the Edge Data Server data folder to persist through
a potential upgrade of your image), add ``-v C:\my\data\folder\Data.Edge:/usr/share/OSIsoft/Data.Edge`` to the command line. You
can add multiple ``-v`` options if you have multiple paths you want to map. For example, you might also want to map the persisted
settings folder to your host, as shown here: 

::

  -v C:\my\data\folder\Data.Edge.PersistedSettings:/usr/share/OSIsoft/Data.Edge.PersistedSettings

Note: If you are using a Microsoft Windows host, ensure that you modify your Docker settings to allow the drive 
you want to share into a container to be shared.

Moving an Image
---------------

As previously discussed, if your goal is to download the image one time from the OSIsoft registry, and then copy it to multiple
devices, you can export and import the image after you have retrieved it. To export the image
from your Docker installation, run the following command (Docker used the *save* command to export):

::

  docker save -o EdgeDataServer.tar edgedev.azurecr.io/osisoft/edgedataserver:x64-latest

The previous command exports the latest x64 image. The file is saved to EdgeDataServer.tar in the working directory of your
command prompt. Copy the exported file to where you would like to run a container, and then execute the following command
to import (load) the image to your target Docker installation:

::

  docker load -i EdgeDataServer.tar

You can use the ``docker image`` and ``docker tag`` commands to rename the image after it has been loaded; depending on your
platform, the name of the image may or might not transfer.

