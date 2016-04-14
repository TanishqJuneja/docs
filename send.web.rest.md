title: Pepipost API Docs v1.0
---

## Send Email - REST

REST/Email send – this API can be use to send emails.

You can call this api using GET as well POST HTTP method.


## Basic Example ( target="_blank"> Click here </a>)

Example call for sending email with required parameters

```
Host https://api.pepipost.com
```

```
Content-Type: application/json
```

```
GET https://api.pepipost.com/api/web.send.rest?
api_key=yoursecretkey
&subject=yourtestsubject
&fromname=yourfromname
&from=from@example.com
&content=YourEmailContent
&recipients=recipient@example.com
```

**<a href="https://docs.pepipost.com/console/#!/Email/get_api_web_send_rest" target="_blank"> Click here </a> to try the above example with our online API console**

	
### Example Response
```
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

## Example with attributes

### Example of sending content personalized email

In order to send personalized content email using Pepipost API, you need to first provide the attribute in your API call along with the place-holders used inside of your HTML content. Like below given example:

**Your API Call**
```
GET /api/web.send.rest?
api_key=yourapikey
&subject=Hi [%NAME%], here is your current balance.
&fromname=Your Company Name
&from=from@example.com
&recipients=mike@example.com,joe@example.com
&content=<p>Hi [%NAME%], your current balance as on today is [%ACCOUNT_BAL%].</p>
&ATT_NAME=Mike,Joe
&ATT_BALANCE=100,200
```

**<a href="https://docs.pepipost.com/console/#!/Email/get_api_web_send_rest" target="_blank"> Click here </a> to try the above example with our online API console**

**NOTE: The "ATT_" is the prefixed, which is required before every attribute name.**

**Mail received by Mike **

```
<p>Hi Mike, your current balance as on today is 100.</p>
```

**Mail received by Joe **

```
<p>Hi Joe, your current balance as on today is 200.</p>
```

## Advance Example

Example of API call with all the parameters.

```
HTTP/1.1
Content-Type: application/json
GET https://api.pepipost.com/api/web.send.rest?
api_key=yoursecretkey
&subject=yourtestsubject
&fromname=yourfromname
&from=from@example.com
&replytoid=replyto@example.com
&X-APIHEADER=ACC123,SE2532
&tags=AccountDeactivation,Verification
&content=YourEmailContent
&recipients=recipient1@example.com,recipient2@example.com
&footer=1
&template=123
&bcc=bcc@example.com
&attachmentid=1,2
&clicktrack=1
&ATT_NAME=NameOfRecipient1,NameOfRecipient2
&ATT_AGE=12,25
```

**<a href="https://docs.pepipost.com/console/#!/Email/get_api_web_send_rest" target="_blank"> Click here </a> to try the above example with our online API console**
	
### Example Response
```
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```




### Parameters
Name | Required | In | Type | Description
--- | --- | --- | --- | ---
api_key |Yes| query | string | Your API Key
fromname |No| query | string | Email Sender name
from |Yes | query | string | From email address
replytoid |No | query | string | Reply to email address
subject |Yes | query | string | Subject of the Email
content |Yes | query | string | Email body in html (to use attributes to display dynamic values such as name, account number, etc. for ex. [% NAME %] for ATT_NAME , [% AGE %] for ATT_AGE etc.)
footer |No | query | boolean | Set &#039;0&#039; or &#039;1&#039; in order to include footer or not
template |No | query | integer | Email template ID
attachmentid |No  | query | string | specify uploaded attachments id (use comma to separate multiple attachmentid).
clicktrack |No  | query | boolean | set ‘0’ or ‘1’ in-order to disable or enable the click-track
opentrack |No  | query | boolean | set open-track value to ‘0’ or ‘1’ in-order to disable or enable
bcc |No  | query | string | Email address for bcc
recipients |Yes  | query | string | Email addresses for recipients (use comma to separate multiple recipients)
ATT_NAME |No  | query | string | Specify attributes followed by ATT_ for recipient to personalized email for ex. ATT_NAME for name, ATT_AGE for age etc. (Multiple attributes are allowed)
X-APIHEADER |No  | query | string | Your defined unique identifier (use comma to separate multiple X-APIHEADER).
tags |No  | query | string | To relate each message. Useful for reports (use comma to separate multiple recipients).


### Responses format
Name | Description
--- | --- 
message | Its can have only 2 values - "SUCCESS" or "ERROR"
errorcode | Pepipost API error code. Its value will be - 0 (zero) in case of success. In case of error it will be non-zero integer value.
errormessage | Error specific error messages. 




