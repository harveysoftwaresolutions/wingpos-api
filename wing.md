This file includes generic parts of the api for wing.

----
# Session Management
  ### Open a session:  
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
    ### Check the status of a session
    
   

