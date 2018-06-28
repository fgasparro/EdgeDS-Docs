Edge Data Store API
===================

The Edge Data Store REST APIs provide programmatic access for data ingress or egress, registration, and administration tasks. 


***********************

``Change password``
-------------------

Change the password you use for the Edge data server. 


**Request**

::

    POST /edge/api/security/ChangePassword


**Parameters**

``string Producer token``
  Your producer token 


::

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

  Task ChangePassword(ChangePasswordData changeRequest);
  
  

**Security**

  Allowed for administrator and user accounts


***********************

Data Server
-----------

``Get stream count``
--------------------

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

  Task<int> GetTotalStreamCountAsync();


**Security**

  Allowed for administrator and user accounts


***********************

``Get data store configuration``
--------------------------------

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

  Task<LocalStoreConfiguration> GetLocalStoreConfigurationAsync();


**Security**

  Allowed for administrator and user accounts


***********************


``Configure stream limits``
---------------------------

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

::

  {
    "streamStorageLimitMb": 0,
    "streamStorageTargetMb": 0
  }
  

**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task SetLocalStoreConfigurationAsync(LocalStoreConfiguration configuration);


**Security**

  Allowed for administrator and user accounts


***********************


``Get metrics``
-----------------

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

  Task<Dictionary<string, string>> GetServerProcessMetricsAsync();


**Security**

  Allowed for administrator and user accounts


***********************


``Get startup parameters``
--------------------------

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

  Task<StartupArguments> GetStartupArgumentsAsync();


**Security**

  Allowed for administrator and user accounts


***********************


``Change startup parameters``
-----------------------------

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

  Task SetStartupArgumentsAsync(StartupArguments arguments);


**Security**

  Allowed for administrator and user accounts


***********************


``Purge event data``
--------------------

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

  Task PurgeEventDataAsync();


**Security**

  Allowed for administrator and user accounts


***********************


``Reset configuration information``
-----------------------------------

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

  Task ResetConfigurationAsync();


**Security**

  Allowed for administrator and user accounts


***********************

``Retrieve server metrics information``
---------------------------------------

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

  Task<Dictionary<string, double>> GetRequestsMetricsAsync();


**Security**

  Allowed for administrator and user accounts


***********************

Egress
------


``List running egress targets``
-------------------------------

Returns a list of running or not running egress targets by target ID. The isRunning flag is used to indicate whether to 
return egress targets that are either running or not running.



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

  Task<EngineParameters> GetTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************


``List egress targets``
-----------------------

Returns a list of all egress targets (both those that are running and those that are not running).


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

  Task<IEnumerable<EngineParameters>> GetTargetsAsync();


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

  


**Security**

  Allowed for administrator and user accounts


***********************



``Get a target``
----------------

Retrieves an individual egress target.


**Request**

::

    GET /edge/api/Egress/omf/targets/{targetId}


**Parameters**

``string Producer token``
  Your producer token 
``string targetId``
  The egress target to retrieve 
  


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task<EngineParameters> GetTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************



``Modify egress target``
------------------------

Modifies an egress target.


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

  Task UpdateTargetAsync(string targetId, string newTargetId, string newDescription, StartupArguments startupArguments);


**Security**

  Allowed for administrator and user accounts


***********************



``Create egress target``
------------------------

Create an egress target. 


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

  Task CreateTargetAsync(string targetId, string description, StartupArguments startupArguments);


**Security**

  Allowed for administrator and user accounts


***********************



``Delete target``
-----------------

Deletes an egress target. 


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

  Task DeleteTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************



``Enable debug dump``
---------------------

Enables a dump of egress data to be written to disk, enabling you to determine exactly what was egressed from the product.
This call is useful when you want to ensure the egress data was actually received by OCS.



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

  


**Security**

  Allowed for administrator and user accounts


***********************



``Add or update egress target``
-------------------------------

Creates an egress target if one does not already exist, or, if the target exists, modifies the egress target. 


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

  Task CreateOrUpdateTargetAsync(string targetId, string description, StartupArguments startupArguments);


**Security**

  Allowed for administrator and user accounts


***********************



``Start an egress target``
--------------------------

Starts a specified egress target. 


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

  Task StartTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************



``Stop an egress target``
-------------------------

Stops a specified egress target. 


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

  Task StopTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************



``Determine if egress target exists``
-------------------------------------

Returns a boolean indicating whether the specified target egress engine exists. 


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

  Task<bool> PingTargetAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************



``Get egress rate``
-------------------

Returns the rate at which data is egressing from the data store. 


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

  Task<Dictionary<(string, string), int>> GetEgressRateAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************


``Get egress rules``
--------------------

Returns a list of rules that are defined for a specified egress target.


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

  Task<IEnumerable<EgressRule>> GetRulesAsync(string targetId);


**Security**

  Allowed for administrator and user accounts


***********************


``Add rule``
-------------

Adds a rule for a specified egress target.


**Request**

::

    POST /edge/api/Egress/omf/targets/{targetId}/Rules


**Parameters**

``string Producer token``
  Your producer token 

::

  {
    "id": "string",
    "name": "string",
    "description": "string",
    "streamFilterId": "string",
    "streamFilterTypeId": "string",
    "streamFilterTags": "string",
    "streamFilterMetadataKey": "string",
    "streamFilterMetadataValue": "string",
    "eventFilter": "string"
  }

**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  Task CreateRuleAsync(string targetId, EgressRule rule);


**Security**

  Allowed for administrator and user accounts


***********************


``Get individual rule``
-----------------------

Returns an individual rule based on the rule ID. 


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

  Task<EgressRule> GetRuleAsync(string targetId, string ruleId);


**Security**

  Allowed for administrator and user accounts


***********************


``Update a rule``
------------------

Updates an egress rule based on the specified rule ID. 


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

  Task UpdateRuleAsync(string targetId, string ruleId, EgressRule updatedRule);


**Security**

  Allowed for administrator and user accounts


***********************


``Delete a rule``
-----------------

Deletes the egress rule specified by the rule ID.


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

  Task DeleteRuleAsync(string targetId, string ruleId);


**Security**

  Allowed for administrator and user accounts


***********************

Ingress
-------



``Ingress data``
-----------------

Ingress data from an OMF message to a specified tenent ID and namespace.


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

  


**Security**

  Allowed for administrator and user accounts


***********************


``Get egress flag``
-------------------

Returns the current state of the egress debug flag. The flag determines whether debug is enabled for the specified 
tenant and namespace.


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

  


**Security**

  Allowed for administrator and user accounts


***********************


``Set egress debug flag``
-------------------------

Sets the state of the egress debug flag. 




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

  


**Security**

  Allowed for administrator and user accounts


***********************

Registration
------------


``Get registration data``
-------------------------

Returns registration data. 


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

  


**Security**

  Allowed for administrator and user accounts


***********************


``Set registration information``
--------------------------------

Writes registration data. 


**Request**

::

    POST /edge/api/Registration


**Parameters**

``string Producer token``
  Your producer token 
  
::

  {
    "lastName": "string",
    "firstName": "string",
    "email": "string",
    "companyName": "string",
    "address": "string",
    "phoneNumber": "string",
    "contactConsent": true
  }


**Response**

  The response includes a status code and a response body.
  

**Response body**

  

**.NET Library**

::

  


**Security**

  Allowed for administrator and user accounts






