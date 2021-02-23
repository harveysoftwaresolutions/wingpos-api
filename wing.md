This file includes api references for the very core functionality of wings:
 - Session managment (With authentication)
 - User management
 - Database management


As long as the server software follows this standard, wing application modules will be able to work with it.

----
# Session Management
  ### Open a session:  
  Only one session may be open per user at once. This will prevent double requests.
  To use a session, a user MUST have the sessionToken.
  Request:  
  
  ```
    {  
      "method": "open_session",
      "nodeID": "<Machine ID>",  
      "authentication": {  
        "user": "<User tokenID>",  
        "secret": "<User secret>"  
      },    
     }
  ```  
  
  Response:  
  
  ```
    {
      "status": {
        
      "sessionToken": "<UUID>"
    }
   ```  
   
  ### Close a session:
  Request:  
  
  ```
    {
      "method": "close_session",
      "sessionToken": "Session Token",
    }
   ```
   
   Response:  
   
   ```
    {
      "sessionStatus": "False"
    }
   ```   
   ### Check if a session is still valid:
   Forcing the closing of a user session is not encouraged, but may be used is a session gets lost.
   Request:  
     
   ```
   {
    "method": "validate_session",
    "sessionToken": "<sessionToken>"
   }
   ```  
   
   Response:
   
   ```
   {
    "sessionToken": "<sessionToken>",
    "sessionStatus": "<sessionStatus>"
   }
   ```
----
# User management
  ### Create a user:
  User management will require a authentication token to validate addition of users. This will be done in wing by using time based 2fa
  Request:
  
  ```
  {
    "method": "create_user",
    "authToken": "<token>"
    "user": "<username>",
    "secret": "<user secret>"
  }
  ```
  
  Response:
  
  ```
  {
    "status": "<Success/Failure>",
    "user": "<new username>",
    "secret": "<user secret>"
  }
   

