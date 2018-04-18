Edge Certificates
=================

For the Edge data store to work correctly with your browser, you must have a security certificate. 

OSIsoft provides a certificate for testing purposes; your IT department probably has its own guidlines and 
procedures for certificate authorities. The certificate is only valid for the *localhost* host. Follow the steps on 
this page to install the OSIsoft certificate.


1. Use Windows Explorer to locate the certificate in the following directory:

   ``***Certificate location***\EdgeRootCert.cer``

2. Double click the certificate file.

   Double clicking the file imports it into the certicate store and the Certificate window displays.
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

   
   


   
   
   
   






