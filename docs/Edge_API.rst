Edge Data Store API
===================

The Edge Data Store REST APIs provide programmatic access for data ingress or egress, registration, and administration tasks. 


***********************

``Change password``
-----------------

Changes the password for the Edge data server. 


**Request**

::

    POST /edge/api/ChangePw


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


**Security**

  Allowed for administrator and user accounts


***********************

Data Server
-----------

``Get stream count``
-------------------

Retrieve the current stream count.


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

``Retrieve the local data store configuration``
-------------------

Retrieve the local data store configuration.


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


``Get ``
-------------------

Write new configuration data. 


**Request**

::

    PUT /edge/api/DataServer/localstoreconfiguration


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

Retrieve current server process metrics.


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

Retrieve a list of current startup parameters


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

Change startup parameters 


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


``Write ??? ``
-------------------

???


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
-------------------

??? 


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

``Retrieve server metrics ``
-------------------

Retrieve ...


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


