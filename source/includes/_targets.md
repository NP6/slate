
#Target

## Get all Targets

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/",
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
  .url("https://backoffice.mailperformance.com/targets/")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets/"
```

<blockquote class="lang-specific json">
  <p>The response from the API is an array structured like this:</p>
</blockquote>
```json
[
  {
    "id": "000MLGPR",
    "creationDate": "2016-04-04T08:55:00Z",
    "lastUpdateDate": "2016-04-04T08:55:00Z",
    "fields": {
      "8103": "test@test.com"
    }
  },
  {
    "id": "000MLGPR",
    "creationDate": "2016-04-04T08:55:00Z",
    "lastUpdateDate": "2016-04-04T08:55:00Z",
    "fields": {
      "8103": "test@test.com"
    }
  }
]
```

This endpoint retrieves all targets.

### HTTP Request

`GET https://backoffice.mailperformance.com/targets`

### Query Parameters

 None

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific Target by ID

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/000MLGPR",
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
  .url("https://backoffice.mailperformance.com/targets/000MLGPR")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/000MLGPR");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets/000MLGPR"
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  Note: <b>bounce</b> and <b>redList</b> can be empty.</p>
</blockquote>

```json
{
  "id": "000MLGPR",
  "creationDate": "2016-04-04T08:55:00Z",
  "lastUpdateDate": "2016-04-25T14:27:00Z",
  "fields": {
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
  },
  "bounce": [
    {
      "field": 8102,
      "type": 1,
      "timestamp": "1465831160",
      "reason": 1
    }
  ],
  "redList": {
    "mail": {
      "timestamp": "1465831160", //optional
      "reason": 1
    },
    "sms": {
      "timestamp": "1465831160", //optional
      "reason": 1      
    }
  }
}
```

This endpoint retrieves a specific target using its ID.

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target ID was not found

### HTTP Request

`GET https://backoffice.mailperformance.com/targets/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the target to retrieve

## Get a specific Target by unicity

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets?unicity=test@test.com",
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
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/getTargetFromUnicity.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/getTargetFromUnicity.php
  </a>
  </p>
</blockquote>

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/targets?unicity=test@test.com")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

<blockquote class="lang-specific java">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/getTargetFromUnicity.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/getTargetFromUnicity.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets?unicity=test@test.com");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/getTargetFromUnicity.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/getTargetFromUnicity.cs
  </a>
  </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/targets?unicity=test@test.com"
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  Note: <b>bounce</b> and <b>redList</b> can be empty.</p>
</blockquote>

```json
{
  "id": "000MLGPR",
  "creationDate": "2016-04-04T08:55:00Z",
  "lastUpdateDate": "2016-04-25T14:27:00Z",
  "fields": {
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
  },
  "bounce": [
    {
      "field": 8102,
      "type": 1,
      "timestamp": "1465831160",
      "reason": 1
    }
  ],
  "redList": {
    "mail": {
      "timestamp": "1465831160", //optional
      "reason": 1
    },
    "sms": {
      "timestamp": "1465831160", //optional
      "reason": 1      
    }
  }
}
```

This endpoint retrieves a specific target using its unicity.

### HTTP Request

`GET https://backoffice.mailperformance.com/targets?unicity=<UNICITY>`

### URL Parameters

Parameter | Description
--------- | -----------
UNICITY | The unicity of the target to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target unicity was not found

## Create or update a Target

```php
<?php
$target =  [
  8101  => "Mr",
  8102  => "Test",
  8103  => "test@test.com"
];

$data = json_encode($target);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets?unicity=test@test.com",
    CURLOPT_CUSTOMREQUEST   => "PUT",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data,
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

<blockquote class="lang-specific php">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/postTarget.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/postTarget.php
  </a>
  </p>
</blockquote>

```java
JSONObject json = new JSONObject();

json.put("8101", "Mr")
    .put("8102", "Test")
    .put("8103", "test@test.com");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/targets?unicity=test@test.com")
  .put(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

<blockquote class="lang-specific java">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/postTarget.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/postTarget.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets?unicity=test@test.com");

var request = new RestRequest(Method.PUT);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddParameter("8101", "Mr", ParameterType.RequestBody);
request.AddParameter("8102", "Test", ParameterType.RequestBody);
request.AddParameter("8103", "test@test.com", ParameterType.RequestBody);

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/postTarget.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/postTarget.cs
  </a>
  </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X PUT "https://backoffice.mailperformance.com/targets?unicity=test@test.com" -d '
{
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
}'
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  Note: <b>bounce</b> and <b>redList</b> can be empty.</p>
</blockquote>

```json
{
  "id": "000MLGPR",
  "creationDate": "2016-04-04T08:55:00Z",
  "lastUpdateDate": "2016-04-25T14:27:00Z",
  "fields": {
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
  },
  "bounce": [
    {
      "field": 8102,
      "type": 1,
      "timestamp": "1465831160",
      "reason": 1
    }
  ],
  "redList": {
    "mail": {
      "timestamp": "1465831160", //optional
      "reason": 1
    },
    "sms": {
      "timestamp": "1465831160", //optional
      "reason": 1      
    }
  }
}
```

This endpoint creates a target or update it if it already exists using its unicity.

### HTTP Request

`PUT https://backoffice.mailperformance.com/targets?unicity=<UNICITY>`

### URL Parameters
Parameter | Description
--------- | -----------
UNICITY | The unicity of the target to find (if not found, will be create)

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
FIELD ID | string | true | FIELD ID is the id of the field. You have to use it to associate a value to a field.

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Create a Target

```php
<?php
$target =  [
  8101  => "Mr",
  8102  => "Test",
  8103  => "test@test.com"
];

$data = json_encode($target);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data,
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

<blockquote class="lang-specific php">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/postTarget.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/postTarget.php
  </a>
  </p>
</blockquote>

```java
JSONObject json = new JSONObject();

json.put("8101", "Mr")
    .put("8102", "Test")
    .put("8103", "test@test.com");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/targets/")
  .post(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

<blockquote class="lang-specific java">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/postTarget.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/postTarget.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/");

var request = new RestRequest(Method.POST);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddParameter("8101", "Mr", ParameterType.RequestBody);
request.AddParameter("8102", "Test", ParameterType.RequestBody);
request.AddParameter("8103", "test@test.com", ParameterType.RequestBody);

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/postTarget.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/postTarget.cs
  </a>
  </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://backoffice.mailperformance.com/targets/" -d '
{
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
}'
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  Note: <b>bounce</b> and <b>redList</b> can be empty.</p>
</blockquote>

```json
{
  "id": "000MLGPR",
  "creationDate": "2016-04-04T08:55:00Z",
  "lastUpdateDate": "2016-04-25T14:27:00Z",
  "fields": {
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
  },
  "bounce": [
    {
      "field": 8102,
      "type": 1,
      "timestamp": "1465831160",
      "reason": 1
    }
  ],
  "redList": {
    "mail": {
      "timestamp": "1465831160", //optional
      "reason": 1
    },
    "sms": {
      "timestamp": "1465831160", //optional
      "reason": 1      
    }
  }
}
```

This endpoint creates a target.

### HTTP Request

`POST https://backoffice.mailperformance.com/targets/`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
FIELD ID | string | true | FIELD ID is the id of the field. You have to use it to associate a value to a field.

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict -- A target with this unicity already exists

## Update a specific Target

```php
<?php
$target =  [
  8101  => "Mr",
  8102  => "Test",
  8103  => "test@test.com"
];

$data = json_encode($target);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/000MLGPR",
    CURLOPT_CUSTOMREQUEST   => "PUT",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data,
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
JSONObject json = new JSONObject();

json.put("8101", "Mr")
    .put("8102", "Test")
    .put("8103", "test@test.com");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/targets/000MLGPR")
  .put(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/000MLGPR");

var request = new RestRequest(Method.PUT);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddParameter("8101", "Mr", ParameterType.RequestBody);
request.AddParameter("8102", "Test", ParameterType.RequestBody);
request.AddParameter("8103", "test@test.com", ParameterType.RequestBody);

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  Note: <b>bounce</b> and <b>redList</b> can be empty.</p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X PUT "https://backoffice.mailperformance.com/targets/000MLGPR" -d '
{
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
}'
```

```json
{
  "id": "000MLGPR",
  "creationDate": "2016-04-04T08:55:00Z",
  "lastUpdateDate": "2016-04-25T14:27:00Z",
  "fields": {
    "8101": "Mr",
    "8102": "Test",
    "8103": "test@test.com"
  },
  "bounce": [
    {
      "field": 8102,
      "type": 1,
      "timestamp": "1465831160",
      "reason": 1
    }
  ],
  "redList": {
    "mail": {
      "timestamp": "1465831160", //optional
      "reason": 1
    },
    "sms": {
      "timestamp": "1465831160", //optional
      "reason": 1      
    }
  }
}
```

This endpoint updates a specific target.

### HTTP Request

`PUT https://backoffice.mailperformance.com/targets/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the target to update

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
FIELD ID | string | true | FIELD ID is the id of the field. You have to use it to associate a value to a field.

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target ID was not found
409 | Conflict -- A target with this unicity already exists

## Add a Target to a Segment

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345",
    CURLOPT_CUSTOMREQUEST   => "POST",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_POSTFIELDS      => null,
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

MediaType mediaType = MediaType.parse("application/json");
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345")
  .post(null)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345");

var request = new RestRequest(Method.POST);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345"
```

<blockquote class="lang-specific json">
<p>No content</p>
</blockquote>

```json
```

This endpoint add a specific target to a specific segment.

### HTTP Request

`POST https://backoffice.mailperformance.com/targets/<targetID>/segments/<segmentID>`

### URL Parameters

Parameter | Description
--------- | -----------
targetID | The ID of the target to add
segmentID | The ID of the segment in wich the target will be add

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target or segment ID was not found
409 | Conflict -- This target is already in the segment

## Remove a Target from a Segment

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345",
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
    .url("https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345");

var request = new RestRequest(Method.DELETE);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X DELETE "https://backoffice.mailperformance.com/targets/000MLGPR/segments/12345"
```

<blockquote class="lang-specific json">
<p>No content</p>
</blockquote>

```json
```

This endpoint removes a specific target from a specific segment.

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target or segment ID was not found
409 | Conflict -- You can't remove a target from a dynamic segment


### HTTP Request

`DELETE https://backoffice.mailperformance.com/targets/<targetID>/segments/<segmentID>`

### URL Parameters

Parameter | Description
--------- | -----------
targetID | The ID of the target to remove
segmentID | The ID of the segment from wich the target will be remove

## Delete a specific Target

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets/000MLGPR",
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
    .url("https://backoffice.mailperformance.com/targets/000MLGPR")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/targets/000MLGPR");

var request = new RestRequest(Method.DELETE);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X DELETE "https://backoffice.mailperformance.com/targets/000MLGPR"
```

<blockquote class="lang-specific json">
<p>No content</p>
</blockquote>

```json
```

This endpoint deletes a specific target.

### HTTP Request

`DELETE https://backoffice.mailperformance.com/targets/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the target to delete

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your target ID was not found



### HTTP Request

`DELETE https://backoffice.mailperformance.com/targets`

### Query Parameters

None

## Delete Targets

```php
<?php
$curl = curl_init();

/*
Unicity criterias are defined in an array, for instance ["email"] or ["email","name"]...
depending on the configuration, thereby:
*/

// Notice that they are exclusives examples, thus only one can be choose depending on the usage.

// If unicity is specified
$value = [["t1@test.com"],["t2@toto.com"]] 
// If Id Target is specified
$value = ["12345","12345"] 
// If segment is specified
$value = XX // XX being the id of the segment, numerical type

$targets = [
    "type" => "unicity", // or id or segment
    "value" => $value
]

$data = json_encode($targets);

$httpHeader = [
    "x-key: YOUR XKEY",
    "Content-Type: application/json",
    "Content-Length: " . strlen($data),
    "Accept: application/vnd.np6.cm.v1",
    "Accept: application/vnd.np6.cm.v1+json"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/targets",
    CURLOPT_CUSTOMREQUEST   => "DELETE",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $data,
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\n\t\"type\": \"unicity\",\n\t\"value\": [\n\t\t[\"t1@test.com\"],\n\t\t[\"t2@toto.com\"]\n\t]\n}");
Request request = new Request.Builder()
  .url("https://api-cm.np6.com/targets")
  .delete(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("Content-Type", "application/json")
  .addHeader("Accept", "application/vnd.np6.cm.v1")
  .build();

Response response = client.newCall(request).execute();

```

```csharp

var client = new RestClient("https://api-cm.np6.com/targets");
var request = new RestRequest(Method.DELETE);
request.AddHeader("Accept", "application/vnd.np6.cm.v1");
request.AddHeader("Content-Type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddParameter("undefined", "{\n\t\"type\": \"unicity\",\n\t\"value\": [\n\t\t[\"t1@test.com\"],\n\t\t[\"t2@test.com\"]\n\t]\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);

```

```shell

curl -X DELETE \
  https://api-cm.np6.com/targets \
  -H 'Accept: application/vnd.np6.cm.v1' \
  -H 'Content-Type: application/json' \
  -H 'x-key: YOUR XKEY' \
  -d '{
    "type": "unicity",
    "value": [
        ["t1@test.com"],
        ["t2@toto.com"]
    ]
}'

```

<blockquote class="lang-specific json">
<p>The request returns a JSON structured like this:</p>
</blockquote>

```json
[  
  {    
    "id": "000JW54T",    
    "unicity": [      
      "t1@test.com"    
      ]  
    },  
    {    
      "id": "000JW54V",    
      "unicity": [      
        "t2@toto.fr"    
        ]  
    } 
]
```

This endpoint deletes targets.

### HTTP Request

`DELETE https://backoffice.mailperformance.com/targets`

### URL Parameters

Parameter | Description
--------- | -----------
None

### Return Codes

Code | Description
---- | -----------
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- The requested targets cannot be found
