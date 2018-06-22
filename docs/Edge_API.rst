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


