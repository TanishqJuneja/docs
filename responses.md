# Pepipost API Responses (<a href="https://github.com/Pepipost/docs/edit/master/responses.md" target="_blank">  Edit </a>)

Currently, we return HTTP code 200 in all our responses, even in case of errors. Except in case of system error it may return HTTP code 500.



### Example of Success Response
```
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

### Example of Failure Response
```
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

# List of Responses (HTTP code & Pepipost errorcode)

#### Success response
Errorcode | Errormessage
--- | ---
0 | (It will be blank in case of success)

#### Error responses
Errorcode | Errormessage
--- | ---
100|Invalid JSON format used in API Call.Hence failed.
101 |Invalid email format replytoid.  
101|Invalid Parameters used in API call.Hence failed.
102|Invalid API key used in API call.Hence authentication failed.
103|Invalid data values used in API call.Hence failed
104|Your free account has expired.Hence failed
105|IP address is not allowed to access this Account.
201|subject not specified
203|content not specified
202|Invalid tag id
204|Invalid from address
205|Invalid From Domain
206|Invalid recipient address
207|Invalid template id
208|Invalid attachment id
209|Multiple template Id not allowed
210|Invalid format for X-APIHEADER found
211|Length of X-APIHEADER cannot be more than 255 characters
212|Invalid mode value
213|Mobile number not specified
214|Mobile text not specified
215|sender ID not specified
401|CDB file creation failed.
402|DBI::MYSQL Query failed
403|Empty mail content.Hence Sending failed
404|Template Processing error.Hence Sending failed
405|MIME::Lite Create message template failed.Hence Sending failed
406|Failed while creating URL MAPPING into database.
407|MD5SUM for client in config not found.Hence failed
408|Job enqueue failed.Please retry after some time
409|Dequeue update credits status in cache failed.
410|Retrieving DKIM sign failed
411|Server Not Rechable Job Archived.
412|Api call could not be processed successfully
500|Account not yet provisioned.
502|Account disabled. Please contact Support.









