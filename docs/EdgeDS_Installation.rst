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


* 1GB RAM or Greater (Highly dependent on the number of streams) 
* Dual-core CPU (X64 or ARM)
* X64 or ARM 32-bit for platform-specific releases, or any platform which supports .Net Core for platform-independent releases.
* Persistent storage (SSD Preferred)
* Edge Data Store files (128 MB required)
* Storage for historical data: TBD


**Supported operating systems**

* Ubuntu 16.04
* Windows 10, Server 2016 
* Windows IoT Core 
* Debian 9 - ARM


**Prerequisites**


The Edge Data Store requires the following software to be installed: 

* Linux - libunwind8 

Other than the packages listed above, the platform-specific Edge Data Store packages contain all of the files 
necessary to run the software. Platform-independent packages are also available; however, these packages require 
.NET Core 2.0 to be installed prior to installing Edge Data Store. 

The platform-specific releases supported by Edge Data Store that do not require pre-installation of .Net 
Core are as follows: 

* Windows 10 x64, 
* Linux x64 
* Linux ARM 32-bit.

To install libunwind8 on Ubuntu or Debian Linux systems, run the following command:

::

  sudo apt-get install libunwind8
  

Windows installation
--------------------

Follow the instructions in this section to install Edge Data Store on Microsoft Windows computers. 

1) Download the Windows msi file from OSIsoft.
2) Use Windows Explorer to navigate to the location where the msi file was downloaded, then double-click the file.
   Follow the prompts to install the software.
3) Using a browser, start the user interface by browsing to the following location:

   ``https://localhost:5000``



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
and writes the changes to permanent storage only when required. 

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


Enable or disable Edge data logging
-----------------------------------

You can enable or disable transaction logging by setting a parameter in the settings file (see `Edge performance tuning`_ for a
description of the settings file). To enable transaction logging, insert the following line in your settings file:

::

  {
    "EnableTransactionLog": 1,
  }

Set the parameter to ``0`` to disable logging.

To enable transaction logging and set the checkpoint rate at the same time, insert the following into your settings file:

::

  {
    “EnableTransactionlog”: 1,
    “CheckpointRateInSec": 30,
  }



Starting the Edge Data Store
----------------------------

**For Microsoft Windows systems:**

By default, Edge Data Store runs as a service on Microsoft Windows systems. The services are started when the installation
completes. 

If you installed Edge Data Store using the default file locations, the
executable file can be found in the following directory:

``C:\Program Files\OSIsoft\EdgeDataStore\OSIsoft.Data.Edge.Server.exe``



**For Linux systems:**

To start the Edge Data Store server on a Linux system, locate the directory in which you extracted the tar file, then
run the following command:

::

  sudo ./OSIsoft.Data.Edge.Server

Optionally, you can specify command-line options to override the default settings. You can view the default settings
with the following command:

::

  sudo ./OSIsoft.Data.Edge.Server --help


Restarting Edge services
------------------------

Occasionally, it might be necessary to restart the Edge services. 

**Windows**

1. From the Start menu, open the *Control Panel*. 
2. Select *Administrative Tools*. 
3. From the Administrative Tools window, open Services. 
4. Select the ``OSIsoft Edge Data Store`` service and then click ``Restart``. 


Command line options
--------------------

You can change certain startup parameters by starting Edge Data Store using command-line options. To view the default 
startup options, run the following command:

**For Windows systems:**

::

  OSIsoft.Data.Edge.Server.exe --help
  

**For Linux systems:**

::

  sudo ./OSIsoft.Data.Edge.Server --help
  
The output of the command resembles the following:

::

  Optional commandline arguments shown below with their default values.

  #####################

  --port 5000 --localstoragelocation C:\ProgramData\OSIsoft\Data.Edge --maxrequestbodysize 196608
  --servercert /path/to/certificate.pfx

  #####################


Startup options are stored in the following file:

::

  C:\ProgramData\OSIsoft\Data.Edge.PersistedSettings\appsettings.json
  
You can edit the settings file and restart Edge Data Store or use the command line options to alter the default behavior.


Edge Certificates
-----------------

.. _CertificateObj: 

In order for the default Edge data store installation to work correctly with your browser or client application, 
you must have two security certificates installed: 

* On the server host, you must have a certificate with an associated private key that is bound to the Edge Data Store service.

* On the client host, you must have a “root” certificate, which the client uses to validate the server’s certificate.

  - In the case of a “self-signed” certificate, the root and server certificate are one and the same.
   
  - In the case of a certificate signed by a certificate authority (CA), the CA root certificate is installed.
   
  - In any case, the root certificate must be “trusted” – the procedure to install a root certificate so that 
    it is “trusted” varies based on the operating system and the application.
     
*	Note that the client host and server host may be the same host (a “localhost” certificate).

For testing purporses, a localhost certificate and associated private key are provided with the Edge Data Store 
installation. The certificate has been signed by a test root authority, and the root authority certificate is also provided.

-  If you do not provide your own server certificate (with its associated private key) the test certificate 
   will be bound to the service by default.
-  If using the test certificate, the root certificate must be installed on the local computer so that it 
   is trusted by your application or browser.
-  The test certificate only supports localhost. If you want to cross the machine boundary (that is, if the 
   Edge Data Store is installed on one computer and you want to access it from a different computer) you must provide 
   a certificate that supports this.

OSIsoft provides certificates for testing purposes only; your IT department probably has its own guidelines and procedures 
for managing digital certificates. You should use the digital certificates recommended by your IT department.
 
The instructions on this page show how to install the OSIsoft root certificate into a trusted location, which in 
turn allows the machine certificate to be validated by a browser or a client application. The default machine 
certificate (provided for testing) is already installed - note that using your own machine certificate is 
possible, and highly recommended for production work. See xxx for details.

Note: Some browsers and applications (such as Mozilla Firefox or Node Red), do not use the certificate store provided 
by the operating system; instead, they use their own. You should search for documentation that is applicable to your 
browser and your operating environment.


**For Microsoft Windows systems:**

1. Use Windows Explorer to locate the certificate. If you used the default installation options, the certificate file
   is located in the following directory:

   ``C:\Program Files\OSIsoft\EdgeDataStore\EdgeRootCert.crt``

2. Double click the certificate file (EdgeRootCert.crt).

   Double clicking the file imports it into the certificate store and the Certificate window displays.
   
3. Click ``Install Certificate``.

   The Certificate Import Wizard window displays.
   
4. Select the ``Local Machine`` radio button then click ``Next``.
5. Select the ``Place all certificates in the following store`` radio button then click ``Browse``.

   The ``Select Certificate Store`` window displays.
6. From the list, select ``Trusted Root Certificate Authority`` then click ``OK``.

   By placing the self-signed certificate in the Trusted Root Certificate Authority location, 
   it will be trusted by the operating system. 
   Leave ``Show Physical Store`` unchecked.
   
7. Click ``Next`` then click ``Finish``.

   A window displays indicating the import was successful. Click ``OK``.
   
8. Close and then restart your browser (if necessary) for the changes to take effect.


**For Linux systems (Ubuntu and Debian)**

1. On your Linux system, copy the security certificate to the certificates folder:

::

  sudo cp EdgeRootCert.crt /usr/local/share/ca-certificates/EdgeRootCert.crt
  
2: Run the following command to update the certificate authority store:

::

  sudo update-ca-certificates


Certificates for browser support
--------------------------------


If your browser reports that the Edge data store site (https://localhost:5000) is not secure, you should follow 
the instructions in this section to supply a security certificate for your browser. The instructions here are specific
to Chrome browsers; however, the procedure should be similar for most browsers.

1. With the Chrome browser open, click the Menu button (located next to the website address bar) then click ``Settings``.
   The Settings section opens in a new tab.

2. Scroll down to the Advanced section of the page and click ``Advanced``.

3. In the Privacy and security section, click ``Manage certificates``.

    Select one of the following depending on the browser you are using:
    
    *If you are using the Chrome browser:*
    
    a. From the Certificates window, select ``Import``.
       The Certificate Import Wizard displays.
       
    b. Click ``Next``.
    
    c. Click the ``Browse`` button, locate the certificate file, and click ``Open''.
    
    d. Click Next.
    
    e. Select ``Place all certificates in the following store`` and select ``Trusted Root Certification Authorities.``
    
    f. Click ``Next`` then click ``Finish``.


    *If you are using the Chromium browser:*
    
    a. Select the ``Authorities`` tab.
    
    b. Click ``Import``.
    
    c. Browse to the location containing your Edge certificate and select it.
    
    d. Click ``Open``.
    
    e. In the *Certificate authority* window, select ``Trust this certificate for identifying websites.``
    
    f. Click ``OK``.
   
After selecting the security certificate, you should stop and then restart your browser.   









