# Actions

## Get all Actions

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/",
    CURLOPT_CUSTOMREQUEST   => "GET",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://v8.mailperformance.com/actions/")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[{
    "type": "mailCampaign",
    "id": "000AB1",
    "name": "Test Campaign",
    "creationDate": "2015-10-30T15:23:00Z",
    "informations": {
        "folder": 123,
        "category": 456,
        "state": 10
    },
    "settings": {
        "templating": {
            "version": "2"
        }
    },
    "scheduler": {
        "type": "asap",
        "startDate": "2015-10-30T15:23:00Z"
    },
    "monitor": {
        "lastSent": {
            "at": "2015-10-30T15:23:00Z"
        }
    }
}, {
    "type": "mailMessage",
    "id": "000AB2",
    "name": "Test Message",
    "creationDate": "2015-10-30T15:23:00Z",
    "informations": {
        "folder": 910,
        "category": 111,
        "state": 50
    },
    "settings": {
        "templating": {
            "version": "4"
        }
    }
}]
```

This endpoint retrieves all actions.

### HTTP Request

`GET https://v8.mailperformance.com/actions`

### Query Parameters

None

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific Campaign

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC",
    CURLOPT_CUSTOMREQUEST   => "GET",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://v8.mailperformance.com/actions/000ABC")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "type": "mailCampaign",
  "id": "000ABC",
  "name": "First",
  "description": null,
  "creationDate": "2016-04-04T08:40:00Z",
  "informations": {
    "folder": 1234,
    "category": 1234,
    "state": 80
  },
  "settings": {
    "field": 1234,
    "culture": "fr-FR",
    "contentFormat": 2,
    "useFormLinkSSL": false,
    "performance": {
      "openingRate": 0,
      "clickRate": 0,
      "unsubscribeRate": 0
    },
    "mp": {
      "use": false,
      "increment": false
    },
    "webAnalyser": null
  },
  "content": {
    "headers": {
      "from": {
        "prefix": "WWC",
        "domain": "defaultdomain",
        "label": "Willy Waller Company"
      },
      "reply": null
    },
    "subject": "New Willy Waller 2006",
    "html": "<html>Content</html>",
    "text": "Content"
  },
  "scheduler": {
    "type": "asap",
    "segments": {
      "selected": [
        12345
      ],
      "excluded": []
    },
    "speed": 0
  }
}
```

This endpoint retrieves a specific action.

### HTTP Request

`GET https://v8.mailperformance.com/actions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your action ID was not found

## Create an Action

```php
<?php
$action = [
    "type"              => "smsCampaign",
    "name"              => "SMS Campaign From Doc",
    "description"       => "This is a description",
    "informations"      => [
        "folder"        => null,
        "category"      => null
    ],
    "scheduler"         => [
        "type"          => "asap"
    ],
    "content"           => [
        "textContent"   => "This is a sms content"
    ]
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
JSONObject from = new JSONObject();
from.put("prefix", "prefix")
    .put("label", "label");

JSONObject reply = new JSONObject();
reply.put("reply", "address@reply.dev");

JSONObject headers = new JSONObject();
headers.put("from", from)
    .put("reply", reply);

JSONObject content = new JSONObject();
content.put("headers", headers)
    .put("subject", "Subject of the message")
    .put("html", "Html message")
    .put("text", "Text message");

JSONObject informations = new JSONObject();
informations.put("folder", 0)
    .put("category", 0);

JSONObject mailMessage = new JSONObject();

mailMessage.put("type", "mailMessage")
    .put("name", "Message a retro valider")
    .put("description", "SMSCampaignFromApi")
    .put("content", content)
    .put("informations", informations);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, mailMessage.toString());
Request request = new Request.Builder()
  .url("https://v8.mailperformance.com/actions/")
  .post(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new
{
    type = "smsCampaign",
    name = "SMS Campaign From Doc",
    description = "This is a description",
    informations = new
    {
        folder = null,
        category = null
    },
    scheduler = new
    {
        type = "asap"
    },
    content = new
    {
        textContent = "This is a sms content"
    }
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
    "type": "smsCampaign",
    "id": "000ABC",
    "name": "SMS Campaign From Doc",
    "description": "This is a description",
    "creationDate": "2016-06-08T11:21:00Z",
    "informations": {
        "folder": 1234,
        "category": 1234,
        "state": 20
    },
    "settings": {
        "field": 1234,
        "smsFormat": 3,
        "smsType": 1
    },
    "content": {
        "textContent": "This is a sms content"
    },
    "scheduler": {
        "type": "asap",
        "segments": {
            "selected": [],
            "excluded": []
        },
        "speed": 0
    }
}
```

This endpoint creates an action.

### HTTP Request

`POST https://v8.mailperformance.com/actions/`

### Query Parameters

#### SMS Campaign

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Action's type ("smsCampaign" for a sms campaign)
name | string | true | Action's name
description | string | true | Action's description
informations | object | true | Object that contains multiple informations
---- folder | int | false | ID of the folder that will contain the sms campaign
---- category | int | false | ID of the category of the campaign
scheduler | object | false | Schedule the sending date
---- type | string | true | String representing the Sending Date ("asap" to lunch it right after validation)
content | object | true | Content of the sms
---- textContent | string | true | Content of the sms but in plain text fomat

#### Mail Campaign

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Action's type ("mailCampaign" for a mail campaing)
name | string | true | Action's name
description | string | true | Action's description
informations | object | true | Object that contains multiple informations
---- folder | int | false | ID of the folder that will contain the sms campaign
---- category | int | false | ID of the category of the campaign
scheduler | object | false | Schedule the sending date
---- type | string | true | String representing the Sending Date ("asap" to lunch it right after validation)
content | object | true | Content of the mail
---- headers | object | true | Email header
-------- from | object | true | Email adress that will be display in field "from"
------------ prefix | string | true | The prefix is the part before the '@' character
------------ domain | string | true | The domain is the part after the '@' character
------------ label | string | true | The category for your mail
-------- reply | string | true | Email adress
---- subject | string | true | Email's subject
---- html | string | true | Content of the mail in HTML format
---- text | string | true | Content of the mail in plain text format
---- Encoding | string | true | Email content encoding

#### SMS Message

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Action's type ("smsMessage" for a sms message)
name | string | true | Action's name
description | string | true | Action's description
informations | object | true | Object that contains multiple informations
---- folder | int | false | ID of the folder that will contain the sms campaign
---- category | int | false | ID of the category of the campaign
content | object | true | Content of the sms
---- textContent | string | true | Content of the sms but in plain text fomat

#### Mail Message

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Action's type ("mailMessage" for a mail message)
name | string | true | Action's name
description | string | true | Action's description
informations | object | true | Object that contains multiple informations
---- folder | int | false | ID of the folder that will contain the sms campaign
---- category | int | false | ID of the category of the campaign
content | object | true | Content of the mail
---- headers | object | true | Email header
-------- from | object | true | Email adress that will be display in field "from"
------------ prefix | string | true | The prefix is the part before the '@' character
------------ domain | string | true | The domain is the part after the '@' character
------------ label | string | true | The category for your mail
-------- reply | string | true | Email adress
---- subject | string | true | Email's subject
---- html | string | true | Content of the mail in HTML format
---- text | string | true | Content of the mail in plain text format
---- Encoding | string | true | Email content encoding

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict

## Update a specific Action

```php
<?php
$action =  [
    "type"              => "mailMessage",
    "name"              => "Message UPDATED",
    "description"       => "Mail Message",
    "informations"      => [
        "folder"        => null,
        "category"      => null
    ],
    "content"           => [
        "text"   => "Text message changed"
    ]
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC",
    CURLOPT_CUSTOMREQUEST   => "PUT",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
JSONObject content = new JSONObject();
content.put("text", "Text message changed");

JSONObject informations = new JSONObject();
informations.put("folder", 0)
    .put("category", 0);

JSONObject updateAction = new JSONObject();

updateAction.put("type", "mailMessage")
    .put("name", "Message UPDATED")
    .put("description", "Mail Message")
    .put("content", content)
    .put("informations", informations);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, updateAction.toString());
Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/actions/000ABC")
    .put(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC");

var request = new RestRequest(Method.PUT);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    type = "mailMessage",
    name = "Message UPDATED",
    description = "Mail Message",
    informations = new {
        folder = null,
        category = null
    },
    content = new {text: "Text message changed"}
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
    "type": "mailMessage",
    "id": "000ABC",
    "name": "Message UPDATED",
    "description": "Mail Message",
    "creationDate": "2016-06-10T08:39:00Z",
    "informations": {
        "folder": 1234,
        "category": 1234,
        "state": 20
    },
    "settings": {
        "field": 1234,
        "culture": "fr-FR",
        "contentFormat": 2,
        "useFormLinkSSL": false,
        "performance": {
            "openingRate": 0,
            "clickRate": 0,
            "unsubscribeRate": 0
        },
        "mp": {
            "use": false,
            "increment": false
        },
        "webAnalyser": null
    },
    "content": {
        "headers": {
            "from": {
                "prefix": "demo",
                "domain": "defaultdomain",
                "label": "demo"
            },    
            "reply": null
        },
        "subject": "demo",
        "html": "<html><head></head><body>demo</body></html>",
        "text": "Text message changed"
    }
}
```

This endpoint update a specific action.

### HTTP Request

`PUT https://v8.mailperformance.com/actions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to update

### Query Parameters

The same as [Create an Action](#create-an-action)

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict

## Delete a specific Action

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC",
    CURLOPT_CUSTOMREQUEST   => "DELETE",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://v8.mailperformance.dev/actions/000ABC")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC");

var request = new RestRequest(Method.DELETE);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

This endpoint delete a specific action.

### HTTP Request

`DELETE https://v8.mailperformance.com/actions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to delete

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found

## Duplicate a specific Action

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC/duplication",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/actions/000ABC/duplication")
    .post()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC/duplication");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
    "type": "smsMessage",
    "id": "000ABD",
    "name": "SMSMessage(1)",
    "description": "SMSMessage",
    "creationDate": "2016-06-10T07:50:00Z",
    "informations": {
        "folder": 1234,
        "category": 1443,
        "state": 10
    },
    "settings": {
        "field": 1234,
        "smsFormat": 3,
        "smsType": 1,
        "countries": []
    },
    "content": {
        "textContent": "Message text."
    }
}
```

This endpoint duplicate a specific action.

### HTTP Request

`POST https://v8.mailperformance.com/actions/<ID>/duplication`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to duplicate

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict
410 | Gone -- Action is no longer available

## Send a specific message Action

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC/targets/0000ABCD",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/actions/000ABC/targets/0000ABCD")
    .post()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC/targets/0000ABCD");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json

```

This endpoint sends a specific message to a target.

### HTTP Request

`POST https://v8.mailperformance.com/actions/<ID>/targets/<TARGETID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to send
TARGETID | The ID of the target

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict

## Validate a specific Action

```php
<?php
$actionValidation =  [
    "fortest"           => true,
    "campaignAnalyser"  => false,
    "testSegments"      => [14091],
    "mediaForTest"      => null,
    "textandHtml"       => false,
    "comments"          => null
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC/validation",
    CURLOPT_CUSTOMREQUEST   => "PUT",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
JSONObject actionValidation = new JSONObject();

actionValidation.put("fortest", true)
    .put("campaignAnalyser", false)
    .put("testSegments", {12345})
    .put("mediaForTest", null)
    .put("textandHtml", false)
    .put("comments", null);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, updateAction.toString());
Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/actions/000ABC/validation")
    .put(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC/validation");

var request = new RestRequest(Method.PUT);

var testSegmentsVal = new int[] {12345};

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    fortest = true,
    campaignAnalyser = false,
    testSegments = testSegmentsVal,
    mediaForTest = false,
    textandHtml = false,
    comments = null
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json
```

This endpoint validate a specific action.

### HTTP Request

`POST https://v8.mailperformance.com/actions/<ID>/validation`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to validate

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
fortest  | bool | false | Specifiy if the validation request is for a test or no
campaignAnalyser  | bool | false | Specifiy of the Campaign Analyser will be used
testSegments | int array | false | Array containing the segments that will be use to test the action
mediaForTest | string | false | Email adress that will be use to test the action
textandHtml  | bool | false | Specify if both text and html version of the action will be send
comments | string | false | Comments

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict
410 | Gone -- Action is no longer available

## Unvalidate a specific Action

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/actions/000ABC/validation",
    CURLOPT_CUSTOMREQUEST   => "DELETE",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/actions/000ABC/validation")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/actions/000ABC/validation");

var request = new RestRequest(Method.DELETE);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json
```

This endpoint unvalidate a specific action.

### HTTP Request

`DELETE https://v8.mailperformance.com/actions/<ID>/validation`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to unvalidate

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict
410 | Gone -- Action is no longer available
