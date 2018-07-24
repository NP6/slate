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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/",
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
  .url("https://api-cm.np6.com/actions/")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://api-cm.np6.com/actions/"
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

`GET https://api-cm.np6.com/actions`

### Query Parameters

None

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

### Action state list

CampaignWorkflowState           |
--------------------------------|
Creation = 10                   |
Created = 20			|
AskingValidation = 38		|
WaitingValidation = 40		|
Validated = 50	    		|
Deleted = 90			|


## Get a specific Campaign

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC",
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
  .url("https://api-cm.np6.com/actions/000ABC")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://api-cm.np6.com/actions/000ABC"
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

`GET https://api-cm.np6.com/actions/<ID>`

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

## Create a SMS Action

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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/",
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
  .url("https://api-cm.np6.com/actions/")
  .post(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/");

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

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://api-cm.np6.com/actions/" -d '
{    
    "type"              : "smsCampaign",
    "name"              : "SMS Campaign From Doc",
    "description"       : "This is a description",
    "informations"      : {
        "folder"        : null,
        "category"      : null
    },
    "scheduler"         : {
        "type"          : "asap"
    },
    "content"           : {
        "textContent"   : "This is a sms content"
    }
}'
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

This endpoint creates a SMS action (Campaign or message).

### HTTP Request

`POST https://api-cm.np6.com/actions/`

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
---- type | string | true | String representing the Sending Date ("asap" to launch it right after validation)
content | object | true | Content of the sms
---- textContent | string | true | Content of the sms but in plain text fomat

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

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict

## Create a mail Action

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://api-cm.np6.com/actions",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => {
   "type":"mailCampaign",
   "name":"Action Mail v4",
   "content":{
      "headers":{
         "from":{
            "prefix":"Test",
            "domain":"defaultdomain",
            "label":"TEST"
         },
         "reply":"test@testreply.fr"
      },
      "subject":"Sujet de la campagne",
      "html":"<html>Bonjour ceci est le html de test</html>",
      "text":"Ceci est la version texte"
   },
   "settings":{
      "templating":{
         "version":4.1
      }
   },
   "informations":{
      "category": XXX // Category ID, if not precised the default value will be used
   },
   "scheduler":{
      "type":"scheduled",
      "startDate":"2017-10-20T14:14:00Z",
      "segments":{
         "selected":[
             XXXX // segment ID
         ],
         "excluded":[

         ]
      },
      "speed":0
   }
},

  CURLOPT_HTTPHEADER => array(
    "Content-Type: application/json",
    "X-KEY: YOUR XKEY"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```java

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, {
	"type": "mailCampaign",
	"name": "Action Mail v4",
	"content": {
		"headers": {
			"from": {
					"prefix": "Test",
					"domain": "defaultdomain",
					"label": "TEST"
			},
			"reply": "test@testreply.fr"
		},
		"subject": "Sujet de la campagne",
		"html" : "<html>Bonjour ceci est le contenu html de test</html>",
		"text" : "Ceci est la version texte"
	},
	"settings" : {
		"templating" : {
			"version": 4.1
		}	
	},
	"informations" : {
		"category" : XXX // Category ID, if not precised the default value will be used
	},
	"scheduler": {
		"type": "scheduled",
		"startDate" : "2017-10-20T14:14:00Z",
		"segments": {
				"selected": [XXXX], // Segment ID
				"excluded": []
		},
		"speed": 0
	}
});
Request request = new Request.Builder()
  .url("https://api-cm.np6.com/actions")
  .post(body)
  .addHeader("X-KEY", "YOUR XKEY")
  .addHeader("Content-Type", "application/json")
  .build();

Response response = client.newCall(request).execute();

```

```csharp

var client = new RestClient("https://api-cm.np6.com/actions");
var request = new RestRequest(Method.POST);
request.AddHeader("Content-Type", "application/json");
request.AddHeader("X-KEY", "YOUR XKEY");
request.AddParameter({
	"type": "mailCampaign",
	"name": "Action Mail v4",
	"content": {
		"headers": {
			"from": {
					"prefix": "Test",
					"domain": "defaultdomain",
					"label": "TEST"
			},
			"reply": "test@testreply.fr"
		},
		"subject": "Sujet de la campagne",
		"html" : "<html>Bonjour ceci est le contenu html de test</html>",
		"text" : "Ceci est la version texte"
	},
	"settings" : {
		"templating" : {
			"version": 4.1
		}	
	},
	"informations" : {
		"category" : XXX
	},
	"scheduler": {
		"type": "scheduled",
		"startDate" : "2017-10-20T14:14:00Z",
		"segments": {
				"selected": [XXXX],
				"excluded": []
		},
		"speed": 0
	}
}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);

```

```shell

curl -X POST \
  https://api-cm.np6.com/actions \
  -H 'Content-Type: application/json' \
  -H 'X-KEY: YOUR XKEY' \
  -d '{
	"type": "mailCampaign",
	"name": "Action Mail v4",
	"content": {
		"headers": {
			"from": {
					"prefix": "Test",
					"domain": "defaultdomain",
					"label": "TEST"
			},
			"reply": "test@testreply.fr"
		},
		"subject": "Sujet de la campagne",
		"html" : "<html>Bonjour ceci est le contenu html de test</html>",
		"text" : "Ceci est la version texte"
	},
	"settings" : {
		"templating" : {
			"version": 4.1
		}	
	},
	"informations" : {
		"category" : XXX
	},
	"scheduler": {
		"type": "scheduled",
		"startDate" : "2017-10-20T14:14:00Z",
		"segments": {
				"selected": [XXXX],
				"excluded": []
		},
		"speed": 0
	}
}'

```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json

{
    "type": "mailCampaign",
    "id": "000XXX",
    "name": "Action Mail v4",
    "description": null,
    "creationDate": "2018-06-08T06:48:00Z",
    "informations": {
        "folder": 204,
        "category": 355,
        "state": 20
    },
    "settings": {
        "templating": {
            "version": 4.1
        },
        "contentFormat": 2,
        "culture": "fr-FR",
        "field": 3085,
        "mp": {
            "use": true,
            "increment": true
        },
        "performance": {
            "openingRate": 0,
            "clickRate": 0,
            "unsubscribeRate": 0
        },
        "useFormLinkSSL": false,
        "webAnalyser": null
    },
    "content": {
        "headers": {
            "from": {
                "prefix": "Test",
                "domain": "defaultdomain",
                "label": "TEST"
            },
            "reply": "test@testreply.fr"
        },
        "subject": "Sujet de la campagne",
        "html": "<html>Bonjour ceci est le contenu html de test</html>",
        "text": "Ceci est la version texte"
    },
    "scheduler": {
        "type": "scheduled",
        "segments": {
            "selected": [
                XXXX
            ],
            "excluded": []
        },
        "speed": 0,
        "startDate": "2017-10-20T14:14:00Z"
}

```

This endpoint creates a mail action (Campaign or message).

### HTTP Request

`POST https://api-cm.np6.com/actions/`

### Query Parameters


#### Mail Campaign

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Action's type ("mailCampaign" or "mailMessage")
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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC",
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
    .url("https://api-cm.np6.com/actions/000ABC")
    .put(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC");

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

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X PUT "https://api-cm.np6.com/actions/000ABC" -d '
{    
    "type"              : "smsCampaign",
    "name"              : "SMS Campaign From Doc",
    "description"       : "This is a description",
    "informations"      : {
        "folder"        : null,
        "category"      : null
    },
    "scheduler"         : {
        "type"          : "asap"
    },
    "content"           : {
        "textContent"   : "This is a sms content"
    }
}'
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

`PUT https://api-cm.np6.com/actions/<ID>`

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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC",
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
    .url("https://api-cm.np6.com/actions/000ABC")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC");

var request = new RestRequest(Method.DELETE);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -X DELETE "https://api-cm.np6.com/actions/000ABC"
```

This endpoint delete a specific action.

### HTTP Request

`DELETE https://api-cm.np6.com/actions/<ID>`

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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/duplication",
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
    .url("https://api-cm.np6.com/actions/000ABC/duplication")
    .post()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/duplication");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://api-cm.np6.com/actions/000ABC/duplication"
```

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

`POST https://api-cm.np6.com/actions/<ID>/duplication`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to duplicate

### Return Codes

Code | Description
---- | -----------
204 | NoContent -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict
410 | Gone -- Action is no longer available

## Send a bulked message

```php

<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api-cm.np6.com/actions/YOUR_ACTION_ID/targets",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "[{'recipient' : {'type': 'id','value': '000ABCDE'}},
		{'recipient' : {'type': 'id','value': '000FGHIJ'}}]",
  CURLOPT_HTTPHEADER => array(
    "Accept: application/json",
    "Content-Type: application/vnd.np6.cm.email-v4",
    "X-Key: YOUR XKEY"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}

?>

```

```java

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/vnd.np6.cm.email-v4");
RequestBody body = RequestBody.create(mediaType, "[{'recipient' : {'type': 'id','value': '000ABCDE'}},{'recipient' : {'type': 'id','value': '000FGHIJ'}}]");
Request request = new Request.Builder()
  .url("http://api-cm.np6.com/actions/YOUR_ACTION_ID/targets")
  .post(body)
  .addHeader("X-Key", "YOUR XKEY")
  .addHeader("Accept", "application/json")
  .addHeader("Content-Type", "application/vnd.np6.cm.email-v4")
  .build();

Response response = client.newCall(request).execute();

```

```csharp

var client = new RestClient("http://api-cm.np6.com/actions/YOUR_ACTION_ID/targets");
var request = new RestRequest(Method.POST);
request.AddHeader("Content-Type", "application/vnd.np6.cm.email-v4");
request.AddHeader("Accept", "application/json");
request.AddHeader("X-Key", "YOUR XKEY");
request.AddParameter("['recipient' : {'type': 'id','value': '000ABCDE'},{'recipient' : {'type': 'id','value': '000FGHIJ'}}]", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);

```

```shell

curl -X POST \
  http://api-cm.np6.com/actions/YOUR_ACTION_ID/targets \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/vnd.np6.cm.email-v4' \
  -H 'X-Key: YOUR XKEY' \
  -d '[
	{
		"recipient" : {
			"type": "id",
			"value": "000ABCDE"
		}
	},
	{
		"recipient" : {
			"type": "id",
			"value": "000FGHIJ"
		}
	}
]'

```


<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this with a conversation ID for each target: </p>
</blockquote>

```json

[
    "CONVERSATION_ID",
    "CONVERSATION_ID"
]

```

This endpoint sends a specific message to a target.

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/targets`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to send


### Request Headers
Name | Value
---- | -----
X-Key | Your XKEY
Content-Type | application/vnd.np6.cm.email-v4
Accept | application/json

## Send a specific message Action

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD",
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
    .url("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD")
    .post()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD"
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json

```

This endpoint sends a specific message to a target.

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/targets/<TARGETID>`

### URL Parameters
Parameter | Description
--------- | -----------
ID | The ID of the action to send
TARGETID | The ID of the target

### Return Codes

Code | Description
---- | -----------
204 | NoContent -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict

## Send a V4 message with overrides

```php
<?php
$overrides = [
    "views" => [
        "html" => "my new HTML"
    ],
    "data" => [
        "my_key" => "my value"
    ]
]
$data = json_encode($overrides);
$curl = curl_init();

$httpHeader = [
    "X-Key: YOUR XKEY",
    "Content-Length: " . strlen($data),
    "Content-Type: application/json",
    "Accept: application/vnd.mperf.v8.message"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD",
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
JSONObject viewOverride = new JSONObject();
viewOverride.put("html", "my new HTML");

JSONObject dataOverride = new JSONObject();
dataOverride.put("my_key", "my value");

JSONObject messageOverride = new JSONObject();
messageOverride.put("views", viewOverride)
    .put("data", dataOverride);

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, messageOverride.toString());
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD")
    .addHeader("Content-Type", "application/json")
    .addHeader("Accept", "application/vnd.mperf.v8.message")
    .addHeader("X-Key", "YOUR XKEY")
    .post(body)
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD");

var request = new RestRequest(Method.POST)
    .AddHeader("Content-Type", "application/json")
    .AddHeader("Accept", "application/vnd.mperf.v8.message")
    .AddHeader("X-Key", "YOUR XKEY")
    .AddBody(new {
        views = new {
            html = "my new HTML"
        },
        data = new { 
            my_key = "my value"
        }
    });

var response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json" \
     -H "Accept: application/vnd.mperf.v8.message" \
     -X POST \
     -d '{"views": {"html": "my new HTML"}, "data": {"my_key": "my value"}}' \
      "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD"
```

<blockquote class="lang-specific json" id="error-code-definitions">
  <p> The full body of the request</p>
</blockquote>
```json
{
    "views": {
        "subject": "My new subject",
        "html": "my new HTML",
        "text": "my new text",
        "fromLabel": "My company",
        "fromPrefix": "mycontact",
        "replyTo": "reply@response.com"                
    },
    "data": {
        "my_key": "my_value" 
    },
    "cc": [
        "cc_target_id"
    ],
    "bcc": [
        "bcc_target_id"
    ]
}
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>
```json
```

This endpoint sends a v4 message to a target. You can override the parameters of the message.
<aside class="notice">
Check the language tab `Body / Response` to get all the parameters of the body to override a message
</aside>

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/targets/<TARGETID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to send
TARGETID | The ID of the target

### Request header

Name | Value
---- | -----
Accept | application/vnd.mperf.v8.message

### Return Codes

Code | Description
---- | -----------
204 | NoContent -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict

## Send a V4 message and return the conversation id

```php
<?php
$overrides = [
    "views" => [
        "html" => "my new HTML"
    ],
    "data" => [
        "my_key" => "my value"
    ]
]
$data = json_encode($overrides);
$curl = curl_init();

$httpHeader = [
    "X-Key: YOUR XKEY",
    "Content-Length: " . strlen($data),
    "Content-Type: application/json",
    "Accept: application/vnd.mperf.v8.message.id"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD",
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
JSONObject viewOverride = new JSONObject();
viewOverride.put("html", "my new HTML");

JSONObject dataOverride = new JSONObject();
dataOverride.put("my_key", "my value");

JSONObject messageOverride = new JSONObject();
messageOverride.put("views", viewOverride)
    .put("data", dataOverride);

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, messageOverride.toString());
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
    .url("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD")
    .addHeader("Content-Type", "application/json")
    .addHeader("Accept", "application/vnd.mperf.v8.message.id")
    .addHeader("X-Key", "YOUR XKEY")
    .post(body)
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD");

var request = new RestRequest(Method.POST)
    .AddHeader("Content-Type", "application/json")
    .AddHeader("Accept", "application/vnd.mperf.v8.message.id")
    .AddHeader("X-Key", "YOUR XKEY")
    .AddBody(new {
        views = new {
            html = "my new HTML"
        },
        data = new { 
            my_key = "my value"
        }
    });

var response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json" \
     -H "Accept: application/vnd.mperf.v8.message.id" \
     -X POST \
     -d '{"views": {"html": "my new HTML"}, "data": {"my_key": "my value"}}' \
      "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD"
```

<blockquote class="lang-specific json" id="error-code-definitions">
  <p> The full body of the request</p>
</blockquote>
```json
{
    "views": {
        "subject": "My new subject",
        "html": "my new HTML",
        "text": "my new text",
        "fromLabel": "My company",
        "fromPrefix": "mycontact",
        "replyTo": "reply@response.com"                
    },
    "data": {
        "my_key": "my_value" 
    },
    "cc": [
        "cc_target_id"
    ],
    "bcc": [
        "bcc_target_id"
    ]
}
```

<blockquote class="lang-specific json">
  <p> The response</p>
</blockquote>
```json
"<conversationID>"
```

This endpoint sends a v4 message to a target. You can override the parameters of the message.
<aside class="notice">
Check the language tab `Body / Response` to get all the parameters of the body to override a message
</aside>

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/targets/<TARGETID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to send
TARGETID | The ID of the target

### Request header

Name | Value
---- | -----
Accept | application/vnd.mperf.v8.message.id

### Return response

The conversation id

```
"36c93e82-dc16-4a72-bc36-63ecd2883f31"
```

See the section [Conversation](?json#conversations)

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found
409 | Conflict

## Send a V4 message with attachments

```php
<?php

$overrides = [
    "views" => [
        "subject" => "My new subject"
    ]
];
$data = json_encode($overrides);
$curl = curl_init();

$httpHeader = [
    "X-Key: YOUR XKEY",
    "Accept: application/vnd.mperf.v8.id.v1"
];

$file_name_with_full_path = realpath('path_to_the_file.jpg');

$nameModel = "model.json"; //On donne un nom au fichier que nous allons crée
$modelFile = fopen($nameModel, "w"); //On crée le fichier model
fwrite($modelFile, $data); //On le remplit
fclose($modelFile); //On le ferme aprés l'avoir remplit

$postfields = array(
    'model' => new CURLFILE($nameModel, "application/json"),
    'attachments' => new CURLFile($file_name_with_full_path, 'image/jpeg', 'filename.jpg')
);

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $postfields
];

try {
    $ok = curl_setopt_array($curl, $opts);

    if( ! $result = curl_exec($curl)) 
    { 
        $err = curl_error($curl);
    } 
}
finally {
    curl_close($curl);
}

?>
```

```java
/* **** Dependencies *****
com.squareup.okhttp3:okhttp:3.4.22
org.apache.clerezza.ext:org.json.simple:0.42
*************************/

JSONObject modelOverride = new JSONObject();
JSONObject viewOverride = new JSONObject();
viewOverride.put("subject", "My new subject");
modelOverride.put("views", viewOverride);

byte[] model = modelOverride.toString().getBytes();

OkHttpClient client = new OkHttpClient();

RequestBody requestBody = new MultipartBody.Builder()
    .setType(MultipartBody.FORM)
    .addFormDataPart("model", "model.json",
            RequestBody.create(MEDIA_TYPE_JSON, model, 0, model.length))
    .addFormDataPart("attachments", "image.jpg",
            RequestBody.create(MEDIA_TYPE_PNG, new File("path_to_the_file.jpg")))
    .build();

Request request = new Request.Builder()
    .url("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD")
    .addHeader("Accept", "application/vnd.mperf.v8.id.v1")
    .addHeader("X-Key", "YOUR XKEY")
    .post(requestBody)
    .build();

try {
    client.newCall(request).execute();
    System.out.println("Mail sent");
}
catch (Exception e){
}
```

```csharp
/* **** Dependencies *****
RestSharp 105.2.3
*************************/

var client = new RestClient("https://api-cm.np6.com/actions/000ABC/targets/0000ABCD");

var request = new RestRequest(Method.POST)
    .AddHeader("Content-Type", "multipart/form-data")
    .AddHeader("Accept", "application/vnd.mperf.v8.id.v1")
    .AddHeader("X-Key", "YOUR XKEY")
	.AddParameter("model", "{'views': {'subject': 'My new subject'}}", "application/json", ParameterType.RequestBody)
	.AddFile("attachments", "path_to_the_file.jpg")
    ;
var response = client.Execute(request);

```

```shell
 curl -H "Accept: application/vnd.mperf.v8.id.v1" \
      -H "X-Key: YOUR XKEY" \
      -X POST \
      -F "attachments=@C:\\path_to_the_file.jpg" \
      -F "model={'views': {'subject': 'My new subject'}};type=application/json" \
      "https://api-cm.np6.com/actions/000ABC/targets/0000ABCD"

```

<blockquote class="lang-specific json" id="error-code-definitions">
  <p> The full body of the request</p>
</blockquote>
```json
------boundary
Content-Disposition: form-data; name="attachments"; filename="maxresdefault.jpg"
Content-Type: image/jpeg

........
------boundary
Content-Disposition: form-data; name="model"
Content-Type: application/json

{
    "views": {
        "subject": "My new subject",
        "html": "my new HTML",
        "text": "my new text",
        "fromLabel": "My company",
        "fromPrefix": "mycontact",
        "replyTo": "reply@response.com"                
    },
    "data": {
        "my_key": "my_value" 
    },
    "cc": [
        "cc_target_id"
    ],
    "bcc": [
        "bcc_target_id"
    ]
}
------boundary

```
<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>
```json
```

This endpoint sends a v4 message to a target with attachments. You can also override the parameters of the message.
<aside class="notice">
Check the language tab `Body / Response` to get all the parameters of the body to override a message
</aside>

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/targets/<TARGETID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action to send
TARGETID | The ID of the target

### Request header

Name | Value
---- | -----
Content-Type | multipart/form-data
Accept | application/vnd.mperf.v8.id.v1

### Request payload
Name | Type | Description
---- | ---- | -----
attachments | image/jpeg | The file to send with the Email
model | application/json | The model to override the Email 

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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/validation",
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
    .url("https://api-cm.np6.com/actions/000ABC/validation")
    .put(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/validation");

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

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://api-cm.np6.com/actions/000ABC/validation" -d '
{
    "fortest"           : true,
    "campaignAnalyser"  : false,
    "testSegments"      : [14091],
    "mediaForTest"      : null,
    "textandHtml"       : false,
    "comments"          : null
}'
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json
```

This endpoint validate a specific action.

### HTTP Request

`POST https://api-cm.np6.com/actions/<ID>/validation`

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
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/validation",
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
    .url("https://api-cm.np6.com/actions/000ABC/validation")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/actions/000ABC/validation");

var request = new RestRequest(Method.DELETE);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -X DELETE "https://api-cm.np6.com/actions/000ABC/validation"
```

<blockquote class="lang-specific json">
  <p> The request doesn't return anything</p>
</blockquote>

```json
```

This endpoint unvalidate a specific action.

### HTTP Request

`DELETE https://api-cm.np6.com/actions/<ID>/validation`

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
