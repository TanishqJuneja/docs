title: Pepipost API Docs v1.0
---

## Send Email - JSON (<a href="https://github.com/Pepipost/docs/edit/master/send.web.json.md" target="_blank">  Edit </a>)

JSON/Email send – this API can be use to send emails.

## Basic example

```
Host: https://api.pepipost.com
```

```
Content-Type: application/json
```

```
POST /api/web.send.json HTTP/1.1
{
    "api_key": "string",
    "email_details": {
        "fromname": "yourfromname",
        "subject": "this is test email subject",
        "from": "from@example.com",
        "content": "<p> hi, this is a test email sent via Pepipost JSON API.</p>"
    },
    "recipients": [
        "recipient@example.com"
    ]
}

```
**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**


### Example Response 

```
HTTP/1.1 200 OK
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

## Example with attributes

### Example of sending content personalized email

In order to send personalized content email using Pepipost API, you need to first provide the attribute in your API call along with the place-holders used inside of your HTML content. Like below given example:

**Your API Call**
```
POST /api/web.send.json HTTP/1.1
{
    "api_key":"yourapikey",
     "email_details":{
      "fromname":"sender name",
      "subject":"test email subject",
      "from":"from@example.com",
      "content":"<p>Hi [%NAME%], your current balance as on today is [%ACCOUNT_BAL%].</p>"
      },
     "recipients":["mike@example.com","joe@example.com"],
      "attributes":{
      "NAME":["Mike","Joe"],
      "ACCOUNT_BAL":["100","200"]
      }
}
```
**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**

**Mail received by Mike **

```
<p>Hi Mike, your current balance as on today is 100.</p>
```

**Mail received by Joe **

```
<p>Hi Joe, your current balance as on today is 200.</p>
```


## Advance example

```
Host: https://api.pepipost.com
```

```
Content-Type: application/json
```

```
POST /api/web.send.json HTTP/1.1
{
    "api_key":"yourapikey",
    "email_details":{
          "fromname":"sender name",
          "subject":"test email subject",
          "from":"from@example.com",
          "replytoid": "replytoid@example.com",
          "tags": "AccountDeactivation, Verification",
          "content":"<p>Hi [%NAME%], This is a test email sent using Pepipost JSON/Email API</p>"
      },
     "X-APIHEADER": ["ID3","ID2"],
     "settings":{
          "footer":"1",
          "clicktrack":"1",
          "opentrack":"1",
          "unsubscribe":"1",
          "bcc":"sac@test.com",
          "attachmentid":"1,3,4",
          "template":"101",
     },
     "recipients":["recipient1@example.com","recipient2@example.com"],
     "attributes":{
          "NAME":["NameOfFirstRecipient","NameOfSecondRecipient"],
          "AGE":["20","30"]
      },
      "files": {
          "attachment_example1.txt": "VGhpcyBpcyB0aGUgY29udGVudCBvZiBhIHRlc3QgZmlsZS4K",
          "attachment_example2.txt": "VGhpcyBpcyB0aGUgY29udGVudCBvZiBhIHRlc3QgZmlsZSAyLgo="
      }
}
```

**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**

** NOTES **

* The fields "NAME" and "AGE" are user defined. One can use any alphanumeric attribute name.
* The fields "attachment_example1.txt" and "attachment_example2.txt" are user defined. One can use any alphanumeric filename.
* The value of field "files" needs to be encoded in base64 encoding format. You can attach various types of files including pdf, png, etc in the same as shown above. However, the above example uses txt file example becauase the base64 for other file types (like pdf) will be large and make the example unreadable.

### Example Response

```
HTTP/1.1 200 OK
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

### Parameters
Name | Required | In | Type | Description
--- | --- | --- | --- | ---
api_key |Yes| query | string | Your API Key
data| Yes | body | [Data](#Data) | Data in JSON format

### Fields
Name | Type | Required | Description
--- | --- | --- | ---
api_key | string | Yes | Your secret API Key
email_details | struct | Yes | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>        <th>description</th>            </tr>    </thead>    <tbody>    <tr>                <td>fromname</td>        <td>string</td>                <td>No</td>                <td>Email Sender name</td>        </tr>    <tr>                <td>subject</td>        <td>string</td>                <td>Yes</td>                <td>subject of the email</td>    </tr>    <tr>                <td>from</td>        <td>string</td>             <td>Yes</td>                   <td>sender email address.</td>        </tr>    <tr>                <td>replytoid</td>        <td>string</td>             <td>No</td>                   <td>email address where recipients reply will be received.</td>        </tr>    <tr>                <td>tags</td>        <td>string</td>                <td>No</td>                <td>This can be use by user to tag/label their emails, in order to categorize for reports and other purposes. Use comma to separate multiple values. </td>        </tr>    <tr>                <td>content</td>        <td>string</td>                <td>Yes</td>                <td></td>        </tr>    </tbody></table>
X-APIHEADER | array[string] | No | This is the user defined ids in order to uniquely identify each emails.
settings | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>        <th>description</th>            </tr>    </thead>    <tbody>    <tr>                <td>footer</td>        <td>boolean</td>                <td>No</td>                <td>To turn on/off the footer addition in the email. User can define footer using dashboard after login.</td>        </tr>    <tr>                <td>clicktrack</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the click tracking of your recipients.</td>        </tr>    <tr>                <td>opentrack</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the open tracking of your recipients.</td>        </tr>    <tr>                <td>unsubscribe</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the unsubscribe link addition in the email.</td>        </tr>    <tr>                <td>bcc</td>        <td>string</td>            <td>No</td>                    <td>Blind Cardbon Copy - a copy of the email will be sent to the email address mentioned here.</td>        </tr>    <tr>                <td>attachmentid</td>        <td>string</td>            <td>No</td>                    <td>To add attachment to the email. User can add attachment using dashboard after login.</td>        </tr>    <tr>                <td>template</td>        <td>integer</td>                <td>No</td>                <td>Template ID of the HTML template which user has created using dashboard, after login.</td>    </tr>    </tbody></table>
recipients | array[string] | Yes | Array of recipients email addresses, to whom the mail will be sent.
attributes | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>                <th>description</th>        </tr>    </thead>    <tbody>    <tr>                <td>NAME</td>        <td>string</td>                <td>No</td>                <td>The key "NAME" is user defined and not fixed. You can put any valid alphanumeric name eg: FIRST_NAME. This needs to be defined per recipients.</td>        </tr>    <tr>                <td>AGE</td>        <td>string</td>                <td>No</td>                <td>The key "AGE" is user defined and not fixed. You can put any valid alphanumeric name eg: FIRST_NAME. This needs to be defined per recipients.</td>        </tr>    </tbody></table>
files | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>            <th>description</th>        </tr>    </thead>    <tbody>    <tr>                <td>your_attachment1.txt</td>        <td>string</td>                <td>No</td>                <td>The key "your_attachment1.txt" is user defined and not fixed. You can put any valid alphanumeric filename for attachment. This needs NOT to be defined per recipients.</td>        </tr>    <tr>                <td>your_attachment2.txt</td>        <td>string</td>            <td>No</td>                    <td>The key "your_attachment2.txt" is user defined and not fixed. You can put any valid alphanumeric filename for attachment. This needs NOT to be defined per recipients.</td>        </tr>    </tbody></table>

	
### Responses format
Name | Description
--- | --- 
message | Its can have only 2 values - "SUCCESS" or "ERROR"
errorcode | Pepipost API error code. Its value will be - 0 (zero) in case of success. In case of error it will be non-zero integer value.
errormessage | Error specific error messages. 

## Integrating with PHP

Its recommended to use Peipost SDK for PHP in order to integrate Pepipost services with applications written in PHP. You can get Pepipost SDK for PHP by <a href="https://github.com/pepipost/pepipost-sdk-php" target="_blank">  clicking here </a> .

### Basic Example

```php
<?php

require_once __DIR__.'/vendor/autoload.php';

use PepipostAPIV10Lib\Controllers\Email;

$email = new Email();

$data = array(
    'api_key'        =>  'yoursecretapikey',
    'recipients'    =>  array('recipient@example.com'),
    'email_details' => array(
        'content'       =>  'this mail is sent via PHP SDK',
        'from'          =>  'from@example.com',
        'subject'       =>  'this mail is sent via PHP SDK',
        'fromname'      =>  'SDK Sender Name ',    
    )
);

try {
    $response = $email->sendJson( $data );
    if(empty($response->errorcode)){
        print "Email sent successfully.\n";
    }
    else {
        print "Email sent Failed.\n";
        print "errormessage(" . $response->errormessage . ") \n";
        print "errorcode(" . $response->errorcode . ").\n";
    }
}
catch(Exception $e){
    print 'Call failed due to unhandled exception/error('. $e->getMessage().')'."\n";
}
```

### Advance Example

```php
<?php

require_once __DIR__.'/vendor/autoload.php';

use PepipostAPIV10Lib\Controllers\Email;

$email = new Email();

$data = array(
    'api_key'   =>  'yoursecretkey',
    'recipients'    =>  array('recipient1@example.com','recipient2@example.com'),
    'email_details' => array(
        'from'          =>  'from@example.com',
        'subject'       =>  'Hi [% NAME %], here is your account balance.',
        'content'       =>  '<p>Hi [%NAME%],</p><p>Your account balance is [% ACCOUNT_BAL %].</p>',
        'fromname'      =>  'SDK Sender Name ',
        'tags'          =>  'AccountDeactivation, Verification',
        'replytoid'     =>  'replyto@example.com',
    ),
    'X-APIHEADER' => array('UserID1','UserID2'),
    'settings' => array(
        'footer'        =>  true,
        'clicktrack'    =>  true,
        'opentrack'     =>  true,
        'unsubscribe'   =>  true,
        'bcc'           =>  'bcc@example.com',
    ),
    'attributes' => array(
        'NAME'          => array('NameOfRecipient1','NameOfRecipient2'),
        'ACCOUNT_BAL'   => array('100','200'),
    ),    
    'files' => array(
        'example_attachment1.txt' => base64_encode(trim(file_get_contents('/path/to/file.txt'))),
        'example_attachment2.pdf' => base64_encode(trim(file_get_contents('/path/to/file.pdf'))),
    ),  
);

try {
    $response = $email->sendJson( $data );
    //var_dump($response);
    if(empty($response->errorcode)){
        print "Email sent successfully.\n";
    }
    else {
        print "Email sent Failed.\n";
        print "errormessage(" . $response->errormessage . ") \n";
        print "errorcode(" . $response->errorcode . ").\n";
    }
}
catch(Exception $e){
    print 'Call failed due to unhandled exception/error('. $e->getMessage().')'."\n";
}
```


## Integrating with Python

Its recommended to use Peipost SDK for Python in order to integrate Pepipost services with applications written in Python. You can get Pepipost SDK for Python by <a href="https://github.com/pepipost/pepipost-sdk-python" target="_blank">  clicking here </a> .

### Basic Example

```python
from PepipostAPIV10Lib.Controllers.Email import *
import json

controller = Email()

#data = ()
data = { 
    'api_key' : 'yoursecretapikey',
    'recipients' : ['recipient1@example.com','recipient2@example.com'],
    'email_details' : { 
        'fromname' : 'sender name',
        'subject' : 'test email subject sent using Pepipost SDK - Python',
        'from' : 'from@example.com',
        'content' : '<p>This is a test email sent using Pepipost JSON/Email Python SDK</p>'
    }   
}

response = controller.send(data)

print response
```

## Integrating with Ruby

Its recommended to use Peipost SDK for Ruby in order to integrate Pepipost services with applications written in Ruby. You can get Pepipost SDK for Ruby by <a href="https://github.com/pepipost/pepipost-sdk-ruby" target="_blank">  clicking here </a> .

### Basic Example

```ruby
require 'pepipost_apiv_10'

data = {
    "api_key"=>"yoursecretapikey",
    "recipients"=> ["recipient1@example.com","recipient2@example.com"],
    "email_details" => {
        "fromname" => "sender name",
        "subject" => "This is a test email sent usig Pepipost SDK for Ruby",
        "from" => "from@example.com",
        "content" => "<p>This is a test email sent using Pepipost SDK for Ruby</p>",
    }
}


email = PepipostApiv10::Email.new
response = email.send data

print response

```

