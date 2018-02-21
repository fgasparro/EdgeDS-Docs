***************
Security  
***************
Edge DS CTP1 includes simple security settings. 
The provided security options are as follows:

1. SSL Transport - required
2. User Authentication for Administration
3. Application validation for Data read/write

The information in this section describes the security features that you might have to interact 
with as a user of the Edge Data Store platform. 

Two basic methods are available for interacting with the system: 

  1) By using interactive mode from a web browser to view and modify settings in the administrative user interface (UI). 
  Using interactive mode, you can make configuration changes or view the current status of the system. 
  
  2) By using non-interactive mode, as a consumer of the APIs. When not using interactive mode, you can develop your
  own client applications. 

The two methods have different requirements and approaches to security, which are described in more detail below.

A secure HTTPS connection is required when using either method. Only HTTPS is supported by the system. HTTPS requires 
the use of digital certificates; how to use and configure certfocates isdescribed in "Certificate Management".

If you are interested in, or having issues with coding in the broswer environment regarding the "Same Origina Policy" or "CORS" see the "Notes on Cross-Origin Resource Sharing" document.

Interactive Session Security
----------------------------

Currently, the interactive Edge Administration site typically running at https://localhost:5000/ (containing the Home, View, Egress, etc. pages) are password protected - you will be prompted to provide a username and password the first time you access a page in a session.

The username and password are fixed; they currently cannot be changed or removed. The username and password are:

	username: edgeadmin
	password: --do we want this in here?--

Note that the password is case sensitive.

Once logged in, you will not be prompted again unless your session ends. The session will end after 15 minutes of inactivity, or you exit the browser.

The exchange of the credentials is protected in transit by HTTPS.

API Security
------------

Currently, the web API(s) supported by the Edge Data Store require clients to provide a token during each call to an API method. This token is a static string key-value pair that must added to the HTTP request headers collection by the client. Clients developed using different technologies will provide different ways for the developer to add the required header, but regardless of the mechanism used, ultimately when the request is sent to the service the token key and value need to be present in the request header, or a 401 (Unauthorized) response will be returned by the service.

The token key and value are fixed; they currently cannot be changed. They are:

	key: producertoken
	value: LzBzgY1zPnxQ55TX6O4WEcj2i1lfL47fDQM57ectmmDjShQvIsQCbMKbKh4i7be

Note that the OMF specification calls for this key to be present - since the Edge Data Store supports OMF, this particular key name was chosen. For the sake of simplicity, regardless of the API, the same key and value are to be used.

Also, note that the API you are choosing may require other header values to be set (e.g OMF specifies a number of additional required headers) which you must still provide - the authentication token only provides a basic security mechanism so that the service can filter calls that don't posses the token.

Again, depending on your choice of client technology, you will have different ways to add the token to the request. For example, .Net (using C#) provides the System.Net.Http.HttpClient class that is often used to make REST API calls - a very simplified example of setting the authentication token in the header is: 

```cs
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


 In some cases, you may be using classes in libraries that encapsulate the underlying web service calls, such as OSIsoft.Data.Http.QiHttpClientFactory or OSIsoft.Data.Http.QiService. In these cases, the classes provide overloaded methods that take an argument of type System.Net.Http.DelegatingHandler. These overloaded methods provide the mechanism to add the authentication token before the service is called.  

 You should, in this case, provide a class derived from DelegatingHandler that will set the request header, and pass a new instance to the overloaded method's DelegatingHandler argument, as shown below:

```cs
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

    // use the above class, for example, to get the services from the QiService class or QiHttpClientFactory class, call the overloaded method with a new instance of your derived DelegateHandler class.
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

Other languages/technologies have other specific ways to set HTTP request headers - please see documentation relevant to your language for more detail.



