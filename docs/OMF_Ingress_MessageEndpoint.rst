OMF API
=======

Edge DS supports the OMF standard for writing data. The route for OMF data is as follows:

https://localhost:5000/edge/omf/tenants/{tenantid}/namespaces/{namespaceid}

Each Edge DS is shipped with a default tenant called "default" and a namespace called "data". 
Utilizing the API additional tenants and namespaces may be created. 
Additionally, each Edge DS is shipped with a single producer token which is to be used in the OMF header for authentication. 



