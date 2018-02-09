**************
Edge DS Admin
**************
.. contents:: Topics in this section: 

Edge Admin
***********

EdgeDS has an admin webpage located at: 

Https://localhost:5000

Home
*****
The functions on the home page are as follows:

Start Data Server - The program is running but the Data Server inside the program can be started. 
Stop Data Server - The program is running but the Data Server inside the program can be stopped.

Data Server Parameters
Changing these settings requires stopping the data server and restarting the .exe or service (CTP1 limitation) 

Port:  Default Port 5000, Any available port can be selected. 
Storage Location: Select any storage location 

Data Server Store
The data server has two configurable settings
1. Per stream storage limit - limits the amount of data stored in each stream in Megabytes. The data store will automatically trim the data oldest first. The default value -1 is unlimited. 
2. Per stream storage target - Is used to calculate the estimated maximum size  

Egress
*******
The Edge Data Server supports two endpoints for Egress, one for PI Connector Relay and one for OSIsoft Cloud Services. 
You can not send data to both PI and OCS at the same time. There is no option for backfilling or any type of historical replay. 
In this version CTP1, if Egress is configured, as data flows into the data store it is immediately sent to the running Egress endpoint.  

PI Egress
You can connect Edge DS to a PI Connector relay by inputing the Relay's Endpoint Address and providing it's OMF Producer token. Submit saves your settings. 
Once your settings are saved you must select start PI Egress. In CTP1, the Edge DS will only send simple types to PI Connectors, the type must have a primary index of time stamp.
 

OCS Egress
In order to send data to OCS you must obtain a cloud services account and configure cloud services to accept data. 
Enter the Endpoint address for OCS and your producer token and select submit. Lastly, start the OCS Egress.  


View
******
The view tool is designed to help end users confirm that data is in their Edge DS. You must select an start and end time in order to return data. 
It may help to select and end time into the future, so that current data is displayed.  

Clear
********


Purge Stream Event Data
*************************
Will remove all the values stored in the streams in the Edge DS without purging the stream configuration. 
This function is helpful if the Data store becomes corrupt and you simply want to return the Data Store to a state where it can collect data without losing configuration. 

Reset Configuration
********************
Returns the Data store to a base configuration. The reset requires that the data server be stopped.
It removes all Egress settings and purges all the stream and stream configuration data from the data store. 


Administration API
*******************
The administration API is a Swagger document. It helps developers to understand what endpoints are available and their parameters for some basic Edge DS functions. 



