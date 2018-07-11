Edge Data Store quick start
===========================


The information in this section shows how to ensure the Edge software is installed and working correctly on your edge device. 

1. On the computer on which Edge Data Store is installed, open a browser and enter the following URL:

::

  https://localhost:5000/home
  

The OSIsoft Edge Administration welcome page displays. If the Administration page does not display, you might have a problem with your security certificate. See Security.

2. Explore the user interface by selecting each of the menu items: Home, View, Egress, Clear, Registration, Change Password,
   Administration API.
   
3. Select the Administraion API page. A new broswer window opens and displays a Swagger UI page that lists each of the
   Edge REST API calls. You can use the Swagger UI to try out any of the Edge REST API calls.
   Note: You must paste a producer token (authorization token) for the API call to complete successfully. A missing or
   incorrect producer token results in a 401 (Not authorized) return code.



