***************
Security  
***************

The information in this section describes the security features you might be required to interact 
with as a user of the Edge Data Store platform. 

Two basic methods are available for interacting with the system:

Interactive mode
   You use interactive mode from a web browser to view and modify settings in the administrative user interface (UI). 
   Using interactive mode, you can make configuration changes or view the current status of the system. 
   
Non-interactive mode  
   You use non-interactive mode when you develop applications as a consumer of the Edge APIs. 

Each method has different requirements and approaches to security, which are described in more detail below.

A secure HTTPS connection is required when using either method. Only HTTPS is supported by the system. HTTPS requires 
the use of digital certificates; how to use and configure certificates is described in "Certificate Management".

If you are interested in the *Same Origin Policy* or *Cross-Origin Resource Sharing* (CORS), or if you are having 
problems coding in the broswer environment, see the "Notes on Cross-Origin Resource Sharing" document.

Interactive mode security
-------------------------

Currently, the interactive Edge administration site (which contains the *Home*, *View*, and *Egress* pages among others) is password 
protected. You are prompted to provide a username and password the first time you access a page in a session. The Edge 
administration site is generally found at: ``https://localhost:5000/``

The username and password for the site are fixed; they currently cannot be changed or removed. The username and password are:

* username: ``edgeadmin``
* password: <to be provided> 

Note that the password is case sensitive.

After you are logged in, you will not be prompted for credentials again unless your session ends. The session ends after 
15 minutes of inactivity or if you exit the browser.

The exchange of the credentials is protected in transit over the network by HTTPS.

API Security
------------

Currently, the web APIs that are supported by the Edge Data Store require clients to provide a token with each call to an 
API method. This token is a static string key-value pair that must be added to the HTTP request headers collection by the 
client. Clients developed using different technologies will provide different ways for the developer to add the required 
header, but regardless of the mechanism used, the token key and value must be present in the request header when the request 
is sent to the service. If the token key and value are not present a 401 (Unauthorized) response is returned by the service.

The token key and value are fixed; they currently cannot be changed. They are:

*  key: ``producertoken``
*  value: ``LzBzgY1zPnxQ55TX6O4WEcj2i1lfL47fDQM57ectmmDjShQvIsQCbMKbKh4i7be``

Note that the OMF specification requires that the key be present. The key name shown above was chosen because the Edge Data 
Store supports OMF. For the sake of simplicity, regardless of the API, you must use the key and value shown above.

Also, note that the API you use might require setting additional header values. OMF, for example, requires a number of additional
required headers. The authentication token provides only a basic security mechanism so that the service is able to filter 
calls that do not contain the token.

Exactly how to add the token to the request depends on the client technology chosen. For example, using C# in a .Net environment 
provides the ``System.Net.Http.HttpClient`` class, which is often used to make REST API calls. A very simplified example of 
setting the authentication token in the header is shown below: 

::

    public class AuthTokenConstants
    {
        // authentication token default
        public const string AuthTokenKey = "producertoken";
        public const string AuthTokenValue = "LzBzgY1zPnxQ55TX6O4WEcj2i1lfL47fDQM57ectmmDjShQvIsQCbMKbKh4i7be";
    }

    public class APIClientClass
    {

    	public async Task CallSomeAPIMethod()
    	{
			HttpClient httpClient = new HttpClient("https://localhost:5000");

			// add the authentication token to the headers. 
			httpClient.DefaultRequestHeaders.Add(
				AuthTokenConstants.AuthTokenKey, AuthTokenConstants.AuthTokenValue);
			
			// make the API call
			await httpClient.PostAsync (...) ...;
		}
	}
```

In some cases, you might be using classes in libraries that encapsulate the underlying web service calls, such as
``OSIsoft.Data.Http.QiHttpClientFactory`` or ``OSIsoft.Data.Http.QiService``. In these cases, the classes provide 
overloaded methods that take an argument of type ``System.Net.Http.DelegatingHandler``. These overloaded methods 
provide the mechanism to add the authentication token before the service is called.  

In the above case, provide a class derived from ``DelegatingHandler`` that sets the request header, and pass a new 
instance to the overloaded method's ``DelegatingHandler`` argument, as shown below:

::


 	// create a class derived from DelegatingHandler, and override SendAsync
 	public class MyAuthTokenDelegatingHandler : DelegatingHandler
    {
        protected async override Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
        {
        	// use the constant token values from above
            if (!request.Headers.Contains(AuthTokenConstants.AuthTokenKey))
            {
                request.Headers.Add(AuthTokenConstants.AuthTokenKey,AuthTokenConstants.AuthTokenValue);
            }

            return await base.SendAsync(request, cancellationToken);
        }
    }

    // use the above class, for example, to get the services from the QiService class or QiHttpClientFactory class, 
       call the overloaded method with a new instance of your derived DelegateHandler class.
    public class UseQiService
    {
        IQiAdministrationService _internalAdminService;
        IQiMetadataService _myMetaDataService;
        
        public void InitializeServices()
        {

            _internalAdminService = QiHttpClientFactory.CreateChannel<OSIsoft.Data.Internal.IQiAdministrationService>(Uri, new MyAuthTokenDelegatingHandler());

           _myMetadataService = QiService.GetMetadataService(Uri, TenantId, MyNamespace, new MyAuthTokenDelegatingHandler());

           // etc
        }
    }
```


With the derived DelegatingHandler, every API call made by the library will have the token as part of the request headers.

Other languages or technologies have other implementation-specific ways to set HTTP request headers. See the documentation 
relevant to your implementation for more details.


