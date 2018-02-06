.. _Introducing_Edge DS_topic:

==============
Introducing Edge Data Store (Edge DS)
==============

.. contents:: Topics in this section:
    :depth: 3


Edge DS is a highly flexible sequential data store that you use to store, retrieve, and analyze data. You 
create and write data to *streams* using a simple REST (*REpresentational State Transfer*) API (*Application 
Programming Interface*). The streams you create can be used to store simple or complex data types to suit 
your application needs. You can define simple or complex indexing to arrange and relate your data. An assortment 
of methods with customizable behaviors are available to read data and easily obtain needed information.

Samples
------------

The best way to get started with Edge DS is to run one or more of the code samples. Code samples are 
provided in a number of different programming languages to illustrate how to easily and effectively 
interact with Edge DS. The code samples can be found in the Edge DS-Samples repository on GitHub. 

Each sample includes a readme which describes the steps required to run the sample and a brief description 
that highlights some of the sample’s functionality. Be sure to read the readme.rst file to understand 
how the sample works.

After you have finished this introduction and worked with one of the samples, refer to 
the :ref:`Quick_start_topic` section, which describes the interaction of 
various Edge DS objects and will help you get started with your own application.

Architecture
------------

A Tenant represents a logical separation of data in Edge DS. All Edge DS's ship with a tenant called "default" 

Tenants are divided into one or more logical units called Namespaces. Each Namespace is distinct and separate from 
other Namespaces, each Edge DS ships with a default namespace of "data". 

.. image:: images/ContainersA.png


Getting help
------------

The following email address is available to participants of the Edge DS
Preview for both product support and feedback:

`EdgeDSSupport@osisoft.com <mailto://EdgeDSSupport@osisoft.com>`__
'For Edge DS feedback please go to' <https://feedback.osisoft.com/forums/906877-edge>

The OSIsoft team will respond to all support requests as
quickly as possible during business hours (Pacific Time).



