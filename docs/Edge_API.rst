Edge Data Store API
===================

The Edge Data Store REST APIs provide programmatic access for data ingress or egress, registration, and administration tasks. 


***********************

``Change password``
-----------------

Change the password you use for the Edge data server. 


**Request**

::

    POST /edge/api/security/ChangePassword


**Parameters**

``string Producer token``
  Your producer token 

{
  "currentPw": "string",
  "pw1": "string",
  "pw2": "string"
}

**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);
  ???

**Security**

  Allowed for administrator and user accounts


***********************

Data Server
-----------

``Get stream count``
-------------------

Returns the number of streams that currently exist in all of the tenants and namespaces.


**Request**

::

    GET /edge/api/DataServer/currenttotalstreamcount


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

``Get data store configuration``
------------------------------

Returns the current configuration of the Edge data store.


**Request**

::


  GET /edge/api/DataServer/localstoreconfiguration  


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Configure stream limits``
--------------------------

Configure the stream target size and maximum size. 
The target size represents the size of most streams you expect to send to the server. The limit size represents 
the maximum stream size that will be sent to the server.

For example, suppost the target size is set to 2 MB and the maaximum size is set to 5 MB. In this case, as the stream
approaches 5 MB in size, the server truncates stream data (from the front of the stream) at 5 MB to achieve the 2 MB target size.


**Request**

::

    PUT /edge/api/DataServer/localstoreconfiguration


**Parameters**

``string Producer token``
  Your producer token 

{
  "streamStorageLimitMb": 0,
  "streamStorageTargetMb": 0
}

**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get metrics``
-------------------

Returns information about the performance of the Edge data server, such as memory usage, CPU usage, and storage usage. 


**Request**

::

  GET /edge/api/DataServer/serverprocessmetrics
    


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get startup parameters``
------------------------

Retrieves a list of parameters that were used to start the Edge data server, such as listener port, the location 
of data storage, and the maximum length of a request that is accepted by the data store.


**Request**

::

    GET /edge/api/DataServer/startuparguments


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Change startup parameters``
-------------------

Modifies the Edge data store startup parameters. Note that you must restart the server in order for changes to 
take effect.


**Request**

::

   PUT /edge/api/DataServer/startuparguments


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Purge event data``
-------------------

Purges all of the event data from all streams, namespaces, and tenants.


**Request**

::

    PUT /edge/api/DataServer/purgeeventdata


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Reset configuration information``
----------------------------------

Resets all egress configuration back to the point where egress is no longer configured.


**Request**

::

    PUT /edge/api/DataServer/resetconfiguration


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

``Retrieve server metrics information``
-------------------------------------

Retrieves metrics information about server data requests.


**Request**

::

    GET /edge/api/DataServer/requestsmetrics


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

Egress
------


``???``
-------------------

Retrieve ???


**Request**

::

    GET /edge/api/Egress/omf/targets/{isRunning}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}/sdsentitiesqueueprocessingparameters


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/sdsentitiesqueueprocessingparameters
        Set SdsStreams Queue Processing Parameters



**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}/sdsvaluesbufferparameters


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/sdsvaluesbufferparameters
        Set SdsStreams Queue Processing Parameters


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    POST /edge/api/Egress/omf/targets/{targetId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    DELETE /edge/api/Egress/omf/targets/{targetId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/sdsegresscontentdump
        Set Egress Content Dump Boolean


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/addorupdate/{targetId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/start


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/stop


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}/ping


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/sdsvaluesegressrate


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}/Rules


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    POST /edge/api/Egress/omf/targets/{targetId}/Rules


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}/Rules/{ruleId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/api/Egress/omf/targets/{targetId}/Rules/{ruleId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    DELETE /edge/api/Egress/omf/targets/{targetId}/Rules/{ruleId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

Ingress
-------



``Get ``
-------------------

Retrieve 


**Request**

::

    POST /edge/omf/tenants/{tenantId}/namespaces/{namespaceId}


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/omf/tenants/{tenantId}/namespaces/{namespaceId}/ingressdebug


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    PUT /edge/omf/tenants/{tenantId}/namespaces/{namespaceId}/ingressdebug


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************

Registration
------------


``Get ``
-------------------

Retrieve 


**Request**

::

    GET /edge/api/Registration


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get ``
-------------------

Retrieve 


**Request**

::

    POST /edge/api/Registration


**Parameters**

``string Producer token``
  Your producer token 


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<QiView> GetViewAsync(string viewId);


**Security**

  Allowed for administrator and user accounts


***********************




