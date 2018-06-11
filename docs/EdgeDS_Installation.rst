.. _Edge_Install_topic:


Edge Data Store installation
============================

Edge Data store is designed to be easy to install with the minimum of system prerequisites. 
There are no dependencies on any other OSIsoft products to complete the installation. 
In addition to standard installation packages, we also provide Docker images for customers
who wish to use application containerization to deploy Edge Data Store. 


Edge Data Store System Requirements
-----------------------------------

**Recommended Hardware**


* 1GB Ram or Greater - Highly dependent on the number of streams 
* Dual-core CPU (X86 or ARM)

* Persistent storage (SSD Preferred)
* Historian files (128 MB required)
* Historical storage - TBD

**Supported operating systems**

* Ubuntu 16.04
* Windows 10, 2016 
* Windows IoT Core 
* Debian 9 - ARM

**Prerequisites**


The Edge Data Store requires the following software to be installed: 

* Linux - libunwind8 

Other than the packages listed above, the platform-specific Edge Data Store packages contain all of the files necessary to run the software. Platform-independent packages are also available; however, these packages require .NET Core 2.0 to be installed prior to installing Edge Data Store. 

Windows installation
--------------------

Follow the instructions in this section to install Edge Data Store on Microsoft Windows computers. 

1) Download the Windows msi file from OSIsoft.
2) Use Windows Explorer to navigate to the location where the msi file was downloaded, then double-click the file.
   Follow the prompts to install the software.
3) Using a browser, start the user interface by browsing to:

   ``localhost:5000``



Linux installation
------------------

Follow the instructions in this section to install Edge Data Store on Windows computers. 

1) Download the tar file from OSIsoft.
2) Navigate to the directory in which the tar file was downloaded and enter the following command   

  ``tar -xvf EdgeDataServerInstall.tar``
   
  You can also specify a directory in which to install:
   
   ``tar -xvf EdgeDataServerInstall.tar -C *your directory*``


Docker image installation
-------------------------

Follow the instructions in this section to install Edge Data Store from a Docker image. 

You install the Docker image by pulling it from the Azure Container Registry. See :ref:`Edge_Install_topic`
for more information.

.. toctree::
   Edge_Docker_Inst

Edge performance tuning
-----------------------

To improve performance, the Edge Data Server writes recent configuration and event data to an in-memory cache
and writes the changes to permanent  storage only when required. 

The Edge Data Server periodically runs a check-point routine that writes all recent configuration 
and event data updates to permanent storage. By default, the checkpoint is performed every 30 seconds.  

Certain scenarios might require adjusting the checkpoint rate to achieve your desired performance and memory footprint. 
Perform the following steps to adjust the periodic checkpoint rate:

1. Create a file named ``settings.json`` in the following folder:

   * For Windows installations: ``C:\ProgramData\OSIsoft\Data.Edge\settings``
   
   * For Linux installations: ``/usr/share/OSIsoft/Data.Edge/settings``

2. The contents of the ``settings.json`` file is a JSON document that resembles the following format:

::

  {
  "CheckpointRateInSec": 30 
  }

3. Modify the original value (30 in this example), to the number of seconds you wish the periodic checkpoint to occur.

4. Restart the Edge Data Server.



Restarting Edge services
------------------------

Occasionally, it might be necessary to restart the Edge services. 

**Windows**

1. From the Start menu, open the *Control Panel*. 
2. Select *Administrative Tools*. 
3. From the Administrative Tools window, open Services. 
4. Select the service and then click Restart. 



Edge Certificates
-----------------

For the Edge data store to work correctly with your browser, you must have two security certificates installed: a machine 
certificate, which permits localhost access, and a root certificate, which permits access to the Edge application.

OSIsoft provides a certificate for testing purposes; your IT department probably has its own guidelines and 
procedures for managing digital certificates. You should use the digital certificates recommended by your IT 
department.

The instructions on this page show how to install the OSIsoft root certificate into a trusted location, which in 
turn allows the machine certificate to be validated by the browser.

Note: Some browsers, such as Mozilla Firefox, do not use the certificate store provided by the operating
system; instead, they use their own. You should search for documentation that is applicable to your browser and your 
operating environment.

**For Microsoft Windows systems:**

1. Use Windows Explorer to locate the certificate in the following directory:

   ``***Certificate location***\EdgeRootCert.cer``

2. Double click the certificate file.

   Double clicking the file imports it into the certificate store and the Certificate window displays.
3. Click ``Install Certificate``.

   The Certificate Import Wizard window displays.
4. Select the ``Local Machine`` radio button then click ``Next``.
5. Select the ``Place all certificates in the following store`` radio button then click ``Browse``.

   The ``Select Certificate Store`` window displays.
6. From the list, select ``Trusted Root Certificate Authority`` then click ``OK``.

   By placing the self-signed certificate in the Trusted Root Certificate Authority location, it will be trusted by the operating system. 
   Leave ``Show Physical Store`` unchecked.
7. Click ``Next`` then click ``Finish``.

   A window displays indicating the import was successful. Click ``OK``.
8. Close and then restart your browser (if necessary) for the changes to take effect.


**For Linux systems**

1. On your Linux system, copy the security certificate file to the certificates folder:

::

  sudo cp EdgeRootCert.cer /etc/ssl/certs
  
2. Create a symbolic link for the certificate ``EdgeRootCert.cer`` 
   This step will also refresh the symbolic links for the rest of the certificates in the folder:

::

  sudo c_rehash /etc/ssl/certs
  
After the OSIsoft root certificate is installed, the software on your system will recognise it.



