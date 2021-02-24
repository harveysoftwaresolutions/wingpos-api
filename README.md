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
 - Errors are made to be specific, clear, and concise



----
# Status object  
There will always be a status in the response  of a request.  
If the ```status``` object is false, further fields are replaced with an ```error``` field and a ```code``` field.   
Errors depend on the method.
The various codes are as follows
- 90-99 (System codes)
  - 90 - ``Bad method``
  - 91 - ``TOTP fail``
  - 92 - 
  - 93 - 
- 100-110 (Session management codes)
  - 100 - ``User does not exist``
  - 101 - ``Invalid user data``
  - 102 - ``Bad token``
  - 103 - ``NodeID already in use``
  - 104 - ``User suspended``
  - 105 - ``Session does not exist``
- 200-210 (User management codes)
  - 200 - ```Invalid username```
  - 201 - ```User already suspended```
  - 202 - ```User secret invalid```
  - 203 - ```Username invalid```
- 300-310 (Database management codes)
  - 300 - ```Database does not exist```
  - 301 - ```Attempt to create a duplicate database```
- 400-410 (Inventory management codes)
  - 300 - ```Invalid item```
  - 301 - ```Null value```
  - 302 - ```Invalid item quantity```
  - 303 - ```1```
- 500-550 (Financial management codes)
- 600-650 (Employee management codes)
- 700-750 (Order management codes)
- 800-850 ()


