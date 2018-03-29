Edge Data Store Egress
======================

The Edge data store collects and stores data from your edge devices. You use the Edge Data Store Egress facility 
to transfer types, streams, and events from the Edge Data Store to either OSIsoft Cloud Services (OCS) or to a 
conventional PI System.

Egress client libraries
-----------------------

Provided with the Edge Data Store software are two NuGet packages:

::

  OSIsoft.Data.Edge.Contracts
  OSIsoft.Data.Edge.Models

The two NuGet packages provide the ability for .NET developers to easily administer and configure the Edge Data Store product.

To use the client libraries, you must first create a QiEdgeService instance, as shown here:

``var edgeServer = new QiEdgeService(new Uri(“https://your_eds_server:5000”));``

You use the ``QiEdgeService`` instance to  access much of the functionality of Edge Data Store. To configure the 
Egress feature of Edge Data Store, create an instance of ``IQiEdgeEgressService`` as shown here:

::

  var egressService = edgeServer.GetEgressService();


.. toctree::

    Edge_Egress_cfg
    Edge_Egress_Rules

