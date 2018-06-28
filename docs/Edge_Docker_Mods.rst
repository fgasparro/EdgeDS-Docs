Docker certificate considerations
=================================

Creating a new Docker image with an HTTPS server certificate
------------------------------------------------------------

By default, the docker image distributed with the Edge Data Store contains a test https server certificate 
with only localhost and the localhost IP addresses as *Subject Alternative Names* (SAN). As described in the 
certificate and installation documentation, in order to connect to Edge Data Store from a remote machine, 
it is necessary to replace this certificate with one that has the server’s hostname or IP address in either 
the common name or as one of the SANs. Generating this certificate is described elsewhere. 

The required certificate file is a .pfx file, which contains both the certificate and the private key. The 
process we will follow will be to create a new Docker image with the server certificate copied into the image, 
and the image modified to have Edge Data Store start with the proper command-line parameters.

Perform the following steps to create a new docker image:

1. Create a new empty folder.

2. Copy the following Dockerfile code into a text file and save it as ``Dockerfile`` in the new empty folder. 
   Replace ``x64`` with ``ARM`` if necessary.

::

    FROM edgedev.azurecr.io/osisoft/edgedataserver:x64-CTP17
    COPY <your certificate name>.pfx /usr/share/OSIsoft/<your certificate name>.pfx
    ENTRYPOINT [“dotnet”, “./OSIsoft.Data.Edge.Server.dll”, “--servercert”, “/usr/share/OSIsoft/<your certificate name>.pfx”]
  
3. Copy the pfx file to the new folder.
4. Open a command prompt and navigate to the new folder.
5. Run the following command:

::

    docker build -t osisoft/edgedataserver_withservercert:x64-CTP17 .
  

6. The new docker image is saved on the local computer as ``osisoft/edgedataserver_withservercert:x64-CTP17``.


Creating a new Docker image with the PI Connector Relay Certificate Trusted
---------------------------------------------------------------------------

The PI Connector Relay endpoint is an https endpoint, which is secured with a self-signed certificate. 
For EDS to trust this certificate, the certificate must be installed into the container’s trusted root 
certificates store. After the certificate is stored in the correct store, Edge Data Store is able to successfully 
egress data to the PI Connector Relay. The process creates a new Docker image with the PI Connector Relay 
self-signed server certificate installed into the trusted root certificates store. To retrieve the 
certificate using the Chrome browser on Windows, navigate to the same URL you will be using as your 
egress endpoint. To the left of the address bar will be either a secure or a not secure note. Click on 
that, then click on certificate to open the certificate properties, select the Details tab, click the 
Copy To File… button, and save the certificate as a base-64 encoded certificate file with a .cer 
extension. Then rename the file to have a .crt extension.

Perform the following steps to create a new docker image:

1. Create a new empty folder.

2. Copy the following Dockerfile code into a text file and save it as Dockerfile in the new empty folder. 
   Replace ``x64`` with ``ARM`` if necessary.

::

  FROM edgedev.azurecr.io/osisoft/edgedataserver:x64-CTP17
  COPY <your certificate name>.crt /usr/local/share/ca-certificates/<your certificate name>.crt
  RUN update-ca-certificates
  
  
3. Copy the PI Connector Relay certificate (.crt) file to the new folder.
4. Open a command prompt and navigate to the new folder.
5. Run the following command:

::

  docker build -t osisoft/edgedataserver_withrelaycert:x64-CTP17 .

6. The new docker image is saved on the local computer as: ``osisoft/edgedataserver_withrelaycert:x64-CTP17``.


Creating a new Docker image with an HTTPS server certificate and the PI Connector Relay certificate trusted
-----------------------------------------------------------------------------------------------------------

To both specify a server certificate *and* trust a PI Connector Relay self-signed server certificate, 
perform the steps listed above for both procedures, except use the image output from the 
first image you created as the base for the second image by modifying the FROM line in the second Dockerfile. 

In other words, assuming you create the new Docker images in the order they are described above (first 
https server cert, then PI Connector Relay cert), the ``FROM`` line in the PI Connector Relay Dockerfile 
would read as: ``FROM osisoft/edgedataserver_withservercert:x64-CTP17``.


