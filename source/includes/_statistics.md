#Statistics

## Get all Aggregated Statistics

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/actions/000ABC/statistics",
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

<blockquote class="lang-specific php">
  <p>go to:
  </br><a href="https://github.com/NP6/CookBook/blob/master/php/createCategory.php" target="_blank">https://github.com/NP6/CookBook/blob/master/php/createCategory.php</a>
  </p>
</blockquote>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/actions/000ABC/statistics")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/actions/000ABC/statistics");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/actions/000ABC/statistics"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "type": "mail",
  "dispatch": {
    "sent": 3000,
    "rejected": {
      "total": 12,
      "redlist": 0,
      "bounces": 0,
      "blacklist": 0,
      "marketingPressure": 0,
      "emptyAddress": 0,
      "exclusions": 0
    }
  },
  "feedback": {
    "reactive": {
      "total": 0,
      "unique": 0
    },
    "opening": {
      "total": 0,
      "opener": {
        "total": 0
      }
    },
    "click": {
      "total": 0,
      "clicker": {
        "total": 0,
        "effective": 0
      }
    },
    "roi": {
      "revenue": 0,
      "commands": 0,
      "products": 0
    },
    "social": {
      "facebook": {
        "shares": 0
      }
    },
    "bounce": {
      "soft": 0,
      "hard": 0,
      "spam": 0
    },
    "redlist": {
      "unsubscribe": {
        "total": 0,
        "form": 0,
        "list": 0
      },
      "complaint": {
        "total": 0,
        "aol": 0,
        "comcast": 0,
        "hotmail": 0,
        "spamcopauto": 0,
        "sspam": 0,
        "yahoo": 0
      }
    }
  }
}
```

This endpoint retrieves statistics of an action.

### HTTP Request

`GET https://backoffice.mailperformance.com/actions/<ID>/statistics`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the action

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your action ID was not found

## Get all NPAI Targets

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/bounces",
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
  .url("https://backoffice.mailperformance.com/targets/bounces")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/bounces");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets/bounces"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[
  {
    "id": "0003Y5O9",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "Requested action not taken: mailbox unavailable5.1.0 - Unknown address error"
        },
        "timestamp": "2008-09-05T19:06:00Z"
      }
    ]
  },
  {
    "id": "0003Y6XT",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "5.0.0 (undefined status)smtp;550 <0616382401@sfr.fr>: Recipient address rejected: User unknown"
        },
        "timestamp": "2008-11-20T10:55:00Z"
      }
    ]
  },
  {
    "id": "0003Y6XU",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "5.1.1 (bad destination mailbox address)smtp;550 5.1.1 unknown or illegal alias: 0661956223@imode.fr"
        },
        "timestamp": "2008-11-20T10:55:00Z"
      }
    ]
  },
  {
    "id": "0003Y6XV",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "5.1.1 (bad destination mailbox address)smtp;550 5.1.1 unknown or illegal alias: 066206620662032528@imode.fr"
        },
        "timestamp": "2008-11-20T10:55:00Z"
      }
    ]
  },
  {
    "id": "0003Y6XX",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "5.0.0 (undefined status)smtp;550 5.2.1 This mailbox has been blocked due to inactivity"
        },
        "timestamp": "2008-11-20T10:55:00Z"
      }
    ]
  },
  {
    "id": "0003Y6XY",
    "bounces": [
      {
        "type": "hardUser",
        "fieldId": 788,
        "detail": {
          "message": "5.0.0 (undefined status)smtp;550 Requested action not taken: mailbox unavailable"
        },
        "timestamp": "2008-11-20T10:55:00Z"
      }
    ]
  }
]
```

This endpoint retrieves all NPAI targets.

### HTTP Request

`GET https://backoffice.mailperformance.com/targets/bounces`

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific NPAI Target

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/actions/000ABC/feedbacks/bounces",
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
  .url("https://backoffice.mailperformance.com/actions/000ABC/feedbacks/bounces")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/actions/000ABC/feedbacks/bounces");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/actions/000ABC/feedbacks/bounces"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[
  {
    "target": "0003YC4O",
    "timestamp": "2009-02-01T22:09:00Z",
    "bounceType": 52
  },
  {
    "target": "000424N1",
    "timestamp": "2009-02-01T22:09:00Z",
    "bounceType": 4
  }
]
```

This endpoint retrieves all specific NPAI Targets of an action.

### HTTP Request

`GET https://backoffice.mailperformance.com/actions/<ID>/feedbacks/bounces`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your action ID was not found

## Get all redlist Targets (mail)

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/redlist/mail",
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
  .url("https://backoffice.mailperformance.com/targets/redlist/mail")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/redlist/mail");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets/redlist/mail"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[
  {
    "id": "0003YB53",
    "timestamp": "2008-12-16T15:26:00Z",
    "origin": 3,
    "detail": {
      "formId": "0000GH"
    }
  },
  {
    "id": "0003YB57",
    "timestamp": "2008-11-25T15:47:00Z",
    "origin": 1,
    "detail": {}
  }
]
```

This endpoint retrieves all mail redlist targets.

### HTTP Request

`GET https://backoffice.mailperformance.com/targets/redlist/mail`

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get all redlist Targets (sms)

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/redlist/sms",
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
  .url("https://backoffice.mailperformance.com/targets/redlist/sms")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/redlist/sms");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets/redlist/sms"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[
  {
    "id": "000ABCD1",
    "timestamp": "2016-06-10T08:01:00Z",
    "origin": 1,
    "detail": {}
  }
]
```

This endpoint retrieves all sms redlist targets.

### HTTP Request

`GET https://backoffice.mailperformance.com/targets/redlist/sms`

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
