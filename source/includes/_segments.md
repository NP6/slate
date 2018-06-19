#Segment

## Get all Segments

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/",
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
  .url("https://api-cm.np6.com/segments/")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://api-cm.np6.com/segments/"
```

<blockquote class="lang-specific json">
  <p>The response from the API is an array structured like this:<br>
  -> First json is for a dynamic segment<br>
  -> Second json is for a static segment</p>
</blockquote>

```json
[
  {
    "type": "dynamic",
    "id": 12345,
    "name": "Test segment dynamic",
    "creation": "2016-04-01T10:22:00Z",
    "expiration": "2016-10-01T10:22:00Z",
    "isTest": true,
    "targetsCount": 5,
    "parentId": 12346 //optional
  },
  {
    "type": "static",
    "id": 12347,
    "name": "Test segment static",
    "creation": "2016-04-01T10:22:00Z",
    "expiration": "2016-10-01T10:22:00Z",
    "isTest": true,
    "targetsCount": 5
  }
]
```

This endpoint retrieves all segments.

### HTTP Request

`GET https://api-cm.np6.com/segments`

### Query Parameters

 None

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific Segment

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/12345",
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
  .url("https://api-cm.np6.com/segments/12345")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/12345");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://api-cm.np6.com/segments/12345"
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  -> This json is for a dynamic segment</p>
</blockquote>

```json
  {
    "type": "dynamic",
    "id": 12345,
    "name": "Test segment dynamic",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z",
    "expiration": "2016-10-01T10:22:00Z",
    "isTest": true,
    "targetsCount": 5,
    "parentId": 12346 //optional
  }
```

<blockquote class="lang-specific json">
  <p>-> This json is for a static segment</p>
</blockquote>

```json
  {
    "type": "static",
    "id": 12345,
    "name": "Test segment dynamic",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z",
    "expiration": "2016-10-01T10:22:00Z",
    "isTest": true,
    "targetsCount": 5
  }
```

This endpoint retrieves a specific segment.

### HTTP Request

`GET https://api-cm.np6.com/segments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the segment to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your segment ID was not found

## Create a Segment

```php
<?php
$segment =  [
  "name"        => "Test segment",
  "description" => "Segment's description",
  "isTest"      => true,
  "type"        => "static",
  "expiration"  => "2026-08-08T12:11:00Z"
];

$data = json_encode($segment);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/",
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
  <a href="https://github.com/NP6/CookBook/blob/master/php/Segments/createSegmentStatic.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/Segments/createSegmentStatic.php
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/Segments/createSegmentDynamic.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/Segments/createSegmentDynamic.php
  </a>
  </p>
</blockquote>

```java
JSONObject json = new JSONObject();

json.put("name", "Test segment")
    .put("description", "Segment's descrption")
    .put("isTest", true)
    .put("type", "static")
    .put("expiration", "2026-08-08T12:11:00Z");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://api-cm.np6.com/segments/")
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
  <a href="https://github.com/NP6/CookBook/blob/master/java/Segments/createSegmentStatic.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/Segments/createSegmentStatic.java
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/Segments/createSegmentDynamic.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/Segments/createSegmentDynamic.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/");

var request = new RestRequest(Method.POST);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    name =  "Test segment",
    description = "Segment's descrption",
    isTest = true,
    type = "static",
    expiration = "2026-08-08T12:11:00Z"
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/Segments/createSegmentStatic.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/Segments/createSegmentStatic.cs
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/Segments/createSegmentDynamic.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/Segments/createSegmentDynamic.cs
  </a>
  </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json" \
     -X POST "https://api-cm.np6.com/segments/" -d '
{
  "name"        : "Test segment",
  "description" : "Segment description",
  "isTest"      : true,
  "type"        : "static",
  "expiration"  : "2026-08-08T12:11:00Z"
}'

```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  -> First json is for a dynamic segment</p>
</blockquote>

```json
{
    "type": "dynamic",
    "id": 12345,
    "name": "Test segment",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z", //optional
    "expiration": "2016-10-01T10:22:00Z", //optional
    "isTest": true, //optional
    "targetsCount": 0, //optional
    "parentId": 12346 //optional
}
```

<blockquote class="lang-specific json">
  <p>-> Second json is for a static segment</p>
</blockquote>

```json
{
    "type": "static",
    "id": 12345,
    "name": "Test segment",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z", //optional
    "expiration": "2016-10-01T10:22:00Z", //optional
    "isTest": true, //optional
    "targetsCount": 0 //optional
}
```

This endpoint creates a segment.

### HTTP Request

`POST https://api-cm.np6.com/segments/`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Segment's name
description | string | true | Segment's description
isTest | boolean | true | If true, the segment can be used for the test phase
type | string | true | Type of the segment ['static' or 'dynamic']
expiration | date | true | Segment's expiration date

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict -- A segment with this name already exists

## Update a specific Segment

```php
<?php
$segment =  [
  "name"        => "Test segment UPDATED",
  "description" => "Segment's description",
  "isTest"      => true,
  "type"        => "static",
  "expiration"  => "2026-08-08T12:11:00Z"
];

$data = json_encode($segment);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/12345",
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

json.put("name", "Test segment UPDATED")
    .put("description", "Segment's descrption")
    .put("isTest", true)
    .put("type", "static")
    .put("expiration", "2026-08-08T12:11:00Z");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://api-cm.np6.com/segments/12345")
  .put(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/12345");

var request = new RestRequest(Method.PUT);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    name = "Test segment UPDATED",
    description = "Segment's descrption",
    isTest = true,
    type = "static",
    expiration = "2026-08-08T12:11:00Z"
});

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X PUT "https://api-cm.np6.com/segments/12345" -d '
{
  "name"        : "Test segment",
  "description" : "Segment description",
  "isTest"      : true,
  "type"        : "static",
  "expiration"  : "2026-08-08T12:11:00Z"
}'
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:<br>
  -> First json is for a dynamic segment</p>
</blockquote>

```json
{
    "type": "dynamic",
    "id": 12345,
    "name": "Test segment",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z", //optional
    "expiration": "2016-10-01T10:22:00Z", //optional
    "isTest": true, //optional
    "targetsCount": 0, //optional
    "parentId": 12346 //optional
}
```

<blockquote class="lang-specific json">
  <p>-> Second json is for a static segment</p>
</blockquote>

```json
{
    "type": "static",
    "id": 12345,
    "name": "Test segment",
    "description": "segment's description",
    "creation": "2016-04-01T10:22:00Z", //optional
    "expiration": "2016-10-01T10:22:00Z", //optional
    "isTest": true, //optional
    "targetsCount": 0 //optional
}
```

This endpoint updates a specific segment.

### HTTP Request

`PUT https://api-cm.np6.com/segments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the segment to update

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Segment's name
description | string | true | Segment's description
isTest | boolean | true | If true, the segment can be used for the test phase
type | string | true | Type of the segment ['static' or 'dynamic']
expiration | date | true | Segment's expiration date

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your segment ID was not found
409 | Conflict -- A segment with this name already exists

## Empty a specific segment

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/12345/targets",
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
  .url("https://api-cm.np6.com/segments/12345/targets")
  .delete()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/12345/targets");

var request = new RestRequest(Method.DELETE);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY"
     -X DELETE "https://api-cm.np6.com/segments/12345/targets"
```

<blockquote class="lang-specific json">
<p>No content</p>
</blockquote>

```json
```

This endpoint empty a specific segment.

### HTTP Request

`DELETE https://api-cm.np6.com/segments/<ID>/targets`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the segment you want to empty

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your segment ID was not found

## Delete a specific Segment

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/12345",
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
  .url("https://api-cm.np6.com/segments/12345")
  .delete()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/12345");

var request = new RestRequest(Method.DELETE);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY"
     -X DELETE "https://api-cm.np6.com/segments/12345"
```

<blockquote class="lang-specific json">
<p>No content</p>
</blockquote>

```json
```

This endpoint deletes a specific segment.

### HTTP Request

`DELETE https://api-cm.np6.com/segments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the segment to delete

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your segment ID was not found

## Update the segment with the target unicities

```php
<?php
$unicities = [
    "unicity1",
    "unicity2",
    "unicity3"
]
$data = json_encode($unicities);
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data),
    "content-type: application/json",
    "Accept: application/vnd.mperf.v8.unicity"
];

$opts = [
    CURLOPT_URL             => "https://api-cm.np6.com/segments/12345/targets",
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
string[] stringArray = {
    "unicity1",
    "unicity2",
    "unicity3"
};
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, Arrays.toString(stringArray));
Request request = new Request.Builder()
  .url("https://api-cm.np6.com/segments/:idSegment/targets")
  .put(body)
  .addHeader("X-Key", "YOUR XKEY")
  .addHeader("Accept", "application/vnd.mperf.v8.unicity")
  .addHeader("Content-Type", "application/json")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://api-cm.np6.com/segments/:idSegment/targets");

var request = new RestRequest(Method.PUT);

request.AddHeader("Content-Type", "application/json")
    .AddHeader("Accept", "application/vnd.mperf.v8.unicity")
    .AddHeader("X-Key", "YOUR XKEY")
    .AddBody([
        "unicity1",
        "unicity2",
        "unicity3"
    ]);

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json" \
     -H "Accept: application/vnd.mperf.v8.unicity" \
     -X PUT \
     -d '["unicity1","unicity2","unicity3"]' \
     "https://api-cm.np6.com/segments/:idSegment/targets"
```


<blockquote class="lang-specific json" id="error-code-definitions">
  <p> The full body of the request</p>
</blockquote>
```json
[
 "unicity1",
 "unicity2",
 "unicity3"
]
```

<blockquote class="lang-specific json">
<p>The response from the API returns the number of target inserted into the segment<br>
</blockquote>

```json
```

This endpoint update a specific segment with targets defined by their unicities.

### HTTP Request

`PUT https://api-cm.np6.com/segments/{id}/targets<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the segment to update

### Query Parameters

Type | Required | Description
---- | -------- | -----------
string array | true | string array of targets unicities

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
400 | Bad Request 
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your segment ID was not found
409 | Conflict
