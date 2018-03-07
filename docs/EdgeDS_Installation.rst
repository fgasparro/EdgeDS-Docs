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

**Supported operating dystems**

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

Follow the instrunctions in this section to install Edge Data Store on Microsoft Windows computers. 

1) Download the Windows msi file from OSIsoft.
2) Use Windows Explorer to navigate to the location where the msi file was downloaded, then double-click the file.
   Follow the prompts to install the software.
3) Using a browser, start the user interface by browsing to:

   ``localhost:5000``



Linux installation
------------------

Follow the instrunctions in this section to install Edge Data Store on Windows computers. 

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


Restarting Edge services
------------------------

Occassionally, it might be necessary to restart the Edge services. 

**Windows**

1. From the Start menu, open the *Control Panel*. 
2. Select *Administrative Tools*. 
3. From the Administrative Tools window, open Services. 
4. Select the service and then click Restart. 



**Linux**

1. Open a Linux command terminal.
2. Enter the following command to obtain a list of running services:

  ``ls /etc/init.d``
     or
  ``ls /etc/rc.d/``

3. Find the name of the service you want to restart.
4. Enter the following command:

   ``sudo systemctl restart`` *service* 
   
   where *service* is the service name to restart.
   
5. Enter your password.




.. toctree::
   Edge_Docker_Inst


