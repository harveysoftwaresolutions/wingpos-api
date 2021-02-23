This file includes generic parts of the api for wing.
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
      "sessionToken": "<UUID>",
      "sessionStatus": "<session status>" //True of False
    }
   ```  
   
  ### Close a session:
  Request:  
  
  ```
    {
      "method": "close_session",
      "sessionToken": "Session Token"
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
    "force": "false"
   }
   ```  
   
   Response:
   
   ```
   {
    "sessionToken": "<sessionToken>",
    "sessionStatus": "<sessionStatus>"
   }
   ```
   
   
   

