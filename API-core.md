# Wingpos-api
Design choices:
 - Access control provided by tokens.
   - User assigned tokens for standard users.
     - This provides access for normal operations.
     - Once authenticated, actions are preformed by a session token.
   - Administrative actions are protected by a rolling key.
     - This allows any workstation with a 2FA key to authenticate for administrative tasks.
       - User management
       - Database management
   - This allows authentication of a station and not an application.
 - Consistent
 - JSON
   - Requests can easily be made in various languages.
 - 








This file includes api references for the very core functionality of wings:
 - Session managment (With authentication)
 - User management
 - Database management


----
# Status object  
There will always be a status in the response  of a request.  
If the ```status``` object is false, further fields are replaced with an ```error``` field.   
Errors depend on the method.





----
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
  ## Suspend a user  
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
  






