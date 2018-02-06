

The purpose of this document is to install Edge DS on Debian 9 on RPI. These
instructions also apply to Ubuntu.

*Prerequisites*

1.  Install Libunwind8 this is available as a package

    1.  Command: sudo apt-get install libunwind8

2.  On the Linux device create the following directories

    1.  /home/%user%/qiedge

3.  Download the Edge DS Bits from the following location:
    <https://osisoft.visualstudio.com/DefaultCollection/QiEdge/QiEdge%20Team/_build/index?context=mine&path=%5C&definitionId=2455&_a=completed>
    select the build ID and then select artifacts and download the drop.zip.

4.  Extract drop.zip

5.  Go to \\drop\\OSIsoft.Data.Edge.Server\\bin\\Release\\netcoreapp2.0

    1.  All the installable files for Edge DS are located here both Windows,
        Linux and Platform Independent

    2.  Go to \\Linux-arm

*Install Edge DS bits on Debian 9 for rPI*

1.  Copy EdgeDataServerInstall_Linux-arm.tar.gz to the Linux device \>/Download

2.  Extract EdgeDataServerInstall_Linux-arm.tar.gz to /Download

3.  Navigate to
    /home/pi/downloads/bin/Relase/netcorapp2.0/linux-arm/EdgeDataServer

4.  Copy all the files in
    /home/pi/downloads/bin/Relase/netcorapp2.0/linux-arm/EdgeDataServer to
    /home/%user%/qiedge

    1.  To launch server - from the command window enter\> **sudo
        ./OSIsoft.Data.Edge.Server**

    2.  Default Data directory is /qi

    3.  In the rPI browser Launch \> <https://localhost:5000/> - You’ll need to
        proceed to an unsafe site since the cert does not match.

    4.  If you’d like to change the data directory, stop the server change the
        directory then restart the server.
