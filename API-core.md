# Session Management
  ## Open a session:  
  Only one session may be open per user at once. This will prevent double requests.
  To create a session, a user MUST have the sessionToken.
  Additionally, sessions will have an inactivity timeout.

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
      "status": "<status>",
      "sessionToken": "<UUID>"
    }
   ```  
  ## Close a session:
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
      "status": "<status>",
      "sessionStatus": "False"
    }
   ```   

   ## Check if a session is still valid:
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
    "status": "<status>"
    "sessionToken": "<sessionToken>",
    "sessionStatus": "<sessionStatus>",
    "nodeID": "<nodeID>"
   }
   ```


----
# User management
  User management will require a authentication token to validate addition of users. This will be done in wing by using time based 2fa. Using a method of 2fa will also enable access control to this part of the api.

  ## Create a user:

  Request:
  
  ```
  {
    "method": "create_user",
    "authToken": "<token>",
    "user": "<username>",
    "secret": "<user secret>",
  }
  ```
  
  Response:
  
  ```
  {
    "status": "<status>",
    "user": "<new username>",
    "secret": "<user secret>"
  }
  ```  

  ## Remove a user:
  This will remove ALL USER DATA FOR THE USER.  
Request:
  ```
  {
    "method": "delete_user",
    "authToken": "<token>",
    "user": "<username to delete>"
  }   
  ```
  Response:
  ```
  {
    "status": "<status>",
    "accountStatus": "<accountStatus">
  }  
  ```

  This will be used to prevent logins from a certain user account.  
  Request:
  ```
  {
    "method": "suspend_user",
    "authToken": "<token>",
    "user": "<user>"
  }
  ```
  Response:  
  ```
  {
    "status": "<status>",
    "accountStatus": "<accountStatus>"
  }
  ```
 
  ## Check the status of a user
  Request:
  ```
  {
    "method": "status_user",
    "user": "<username>"
  }
  ```
  Response:  
  ```
  {
    "status": "<status>",
    "userStatus": "<userstatus>"
  }
  ```
  ## Export user data   
  I'm not sure how this will pass data.  
  Request:
  ```
  {
    "method": "export_user",
    "authToken": "<token>",
    "user": "<user>"
  }
  ```
  Response:
  ```
  {
    "status": "<status>",
    "userdata": {}
  }
  ```

  ----

  # Database management
  Database management has access control.
  ## Create a new database
  Request:
  ```
  {
    "method": "create_database",
    "authToken": "<token>",
    "dbname": "<dbname>"
  }
  ```
  Response:
  ```
  {
    "status": "<status>"
  }
  ```
  ## Delete a database
  Request:
  ```
  {
    "method": "delete_database",
    "authToken": "<token>",
    "dbname": "<dbname>"
  }
  ```
  Response:
  ```
  {
    "status": "<status>"
  }
  ```
  ## Change the active database
  Request:
  ```
  {
    "method": "select_database",
    "authToken": "<token>",
    "dbname": "<dbname>"
  }
  ```
  Response:
  ```
  {
    "status": "<status>",
    "activedb": "<dbname>"
  }
  ```

  






