Certificate Management
======================

This section describes how server certificates are used and validated in the Edge Historian, and how
certificates should be created and managed. 

Description of Certificate Usage
--------------------------------

Server-side certificates are used by HTTPS services both for encryption of the data being transmitted
across the wire, and for validation that the host a client is connecting to is the host they expected
to connect to.

On startup, the Edge Historian binds to port 5000 on the local machine. With HTTPS enabled in the
release build of the product, a server certificate along with private key (which combined form the
pfx file) are associated with this connection. Typically, this server certificate has been signed
using a certificate authority certificate (CA). This CA is trusted by the client. By validating that 1.
the signature on the server certificate was generated by a trusted CA, 2. the domain name or IP address
the client is connecting to matches either the subject name or one of the subject alternative names
listed in the server certificate, and 3. the current date is between the valid from and valid to
dates listed in the certificate, the client is assured that the connection is to the server it was
expecting to connect to and is encrypted.

Because the CA certificate is what is trusted by the client, any server certificate signed by this CA
is considered valid. Therefore, it is possible to have a new server certificate generated nightly,
signed by this same CA certificate, and have this new server certificate be trusted by any client that
trusts the CA certificate.

In order to sign a server certificate, the CA certificate's private key is required. However, to
validate a server certificate's signature (like a client would do), only the public key is required.
With only the public key an attacker is not able to generate a valid server certificate signature.
Therefore, the public key certificate can be distributed to client applications and can be installed
in the trusted root authorities certificate store without worry that an attacker could impersonate
the Edge Historian.

In the case of the Edge Historian, we are embedding a server certificate into the product binaries.
This server certificate could be used as a permanent solution in certain scenarios. There are two
requirements for using this certificate as a permanent solution. The first requirement is that the
user regularly updates the Edge Historian. The server certificate will have a 2-year expiration from
the build date, so some time before those two years are up, the historian will have to be updated or
the certificate will have expired. The second requirement is that the Edge Historian be accessed only
from the local system. Because we don't know the hostnames or IP addresses that will be assigned to
servers hosting the Edge Historian, the only subject alternative names we can put on the server
certificate are localhost, 127.0.0.1, and ::1 (the IPv6 localhost IP address). Any client accessing
the Edge Historian using a different hostname or IP address will fail validation with a mismatched
domain name error. Of course, the exception to these requirements is if the client does not validate
or only partially validates the server certificate.

The more secure and flexible solution is for a user to create their own server certificate. The user
can either create a self-signed server certificate, or can create a self-signed CA certificate and
use that to generate a server certificate. Once that is available, the user can install the server
certificate onto the Edge Historian server and specify via a command line parameter the location
of that certificate file (.pfx). At this time, we do not support server certificates that require
a password to read.

Using the Edge Historian With Certificates
------------------------------------------

When the Edge Historian starts up, it looks for a --servercert <file> option on the command line. If
that option exists, the file specified (which should be a .pfx file with no password) is loaded and
used as the server certificate. If that option is not specified, there is a certificate embedded in
the application binaries that is used. The exact embedded certificate used depends on how the
application was built.

1. Placeholder Certificate

   The Edge Historian Server Visual Studio project has a certificate embedded in the project as a resource.
   This certificate was issued once and should remain unchanged until it expires on 9/29/2019. This
   certificate is intended to be used only in development; in other words, when building and running on a
   developer's machine. This certificate has a subject alternative names of localhost, 127.0.0.1, and ::1,
   and was issued (signed) by our CA certificate.

2. Release Certificate
   The automated build process which runs in Visual Studio Online generates a server certificate with 
   each build and replaces the embedded resource that exists in the Visual Studio project. This certificate
   expires two years after the build date. Besides the expiration date (and the common name), this
   certificate is identical to the placeholder certificate. The reason this certificate is issued is because
   we'd like newly built packages to have a full two years before expiration, rather than two years from the
   date the single placeholder certificate was issued.

   In both cases above, the CA certificate must be trusted by any client application that
   communicates with the Edge Data Historian. To establish this trust, the user of the client application 
   must add the OSIsoft-generated security certificate (ca.cert.crt or ca.cert.pem - not the .pfx or the .key.pem) 
   to the trusted root certificate authorities store.
   Because the file contains a root security certificate, contact OSIsoft to obtain a copy.
   
   Additionally, in both cases above, because we have no knowledge of a user's network topology or machine
   naming conventions, we have no way of adding the historian's hostname to the certificate. Therefore,
   only local client applications will properly validate the server certificate. In order to use a remote
   hostname, a user-supplied certificate needs to be provided.

   In the case where the certificate is user-supplied, the CA issuing that certificate should be trusted. This
   could be a user-supplied self-signed CA certificate, or a certificate issued by a well-known CA.

Creating Certificates
---------------------

There are quite a few steps in creating CA and server certificates, described below. These steps assume the
existence of OpenSSL configuration files, also located at $/OSIsoft.Data.Edge.Server/Certificates. The config
files are named openssl.server.cnf and openssl.ca.cnf. You may need to open these files and modify them.

1. Generate CA private key (supply a password, the one I've used already is in a comment at the top of the
   openssl.ca.cnf config file):
   `openssl genrsa -aes256 -out ca.key.pem 4096`.
2. Generate self-signed CA certificate with a 30-year expiration:
   `openssl req -config openssl.ca.cnf -key ca.key.pem -new -x509 -days 10957 -sha256 -extensions v3_ca -out
   ca.cert.pem`.  
   (At this point, the ca.cert.pem file can be duplicated into ca.cert.crt, as .crt is the extension Windows
   recognizes as keyless certificate files).
3. Verify CA certificate signing request:
   `openssl x509 -in ca.cert.pem -text -noout`.
4. Generate CA certificate .pfx file (combination of public and private key):
   `openssl pkcs12 -export -in ca.cert.pem -inkey ca.key.pem -out ca.pfx`.
5. Generate server private key:
   `openssl genrsa -out localhost.key.pem 2048`.
6. Generate server certificate signing request (unsigned server certificate):
   `openssl req -config openssl.server.cnf -key localhost.key.pem -new -sha256 -out localhost.csr.pem`.
7. Sign server CSR with CA private key:
   `openssl ca -config openssl.server.cnf -extensions server_cert -days 730 -notext -md sha256
   -in localhost.csr.pem -out localhost.cert.pem`.
8. Verify server certificate:
   `openssl x509 -in localhost.cert.pem -text -noout`.
9. Generate server certificate pfx (don't include an export password unless the historian has been modified to
   allow for passwords on the server .pfx file):
   `openssl pkcs12 -export -in localhost.cert.pem -inkey localhost.key.pem -out localhost.pfx`.
  
  
