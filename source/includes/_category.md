#Category

##Get all Categories

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/categories",
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
  .url("https://v8.mailperformance.com/categories")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/categories");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
[
  {
    "id": 1234,
    "name": "non_categorisee",
    "description": null,
    "creationDate": "2016-04-01T10:22:00Z"
  },
  {
    "id": 1235,
    "name": "Old",
    "description": null,
    "creationDate": "2016-06-15T07:54:00Z"
  }
]
```

This endpoint retrieves all categories.

### HTTP Request

`GET https://v8.mailperformance.com/categories`

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific Category

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/categories/1234",
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
  .url("https://v8.mailperformance.com/categories/1234")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/categories/1234");

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
  "id": 1234,
  "name": "non_categorisee",
  "description": null,
  "creationDate": "2016-04-01T10:22:00Z"
}
```

This endpoint retrieves a specific category.

### HTTP Request

`GET https://v8.mailperformance.com/categories/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the category to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your category ID was not found

## Create a specific Category

```php
<?php
$category = [
    "name"                         => "New",
    "description"                  => "Category for new campaign"
];

$data = json_encode($category);

$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY",
    "content-type: application/json",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/categories/",
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

<blockquote class="lang-specific php">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/createCategory.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/createCategory.php
  </a>
  </p>
</blockquote>

```java
JSONObject category = new JSONObject();

category.put("name", "New")
    .put("description", "Category for new campaign");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");

RequestBody body = RequestBody.create(mediaType, category.toString());
Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/categories/")
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
  <a href="https://github.com/NP6/CookBook/blob/master/java/createCategory.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/createCategory.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://v8.mailperformance.com/categories/");

var request = new RestRequest(Method.POST);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    name: "New",
    description: "Category for new campaign"
  });

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/createCategory.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/createCategory.cs
  </a>
  </p>
</blockquote>

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>


```json
{
  "id": 1234,
  "name": "New",
  "description": "Category for new campaign",
  "creationDate": "2016-06-15T07:54:00Z"
}
```

This endpoint creates a category.

### HTTP Request

`POST https://v8.mailperformance.com/categories/`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Category's name
description | string | false | Category's description

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict -- A category with this name already exists

## Update a specific Category

```php
<?php
$category = [
    "name"                         => "Updated",
    "description"                  => "Category for new campaign"
];

$data = json_encode($category);

$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY",
    "content-type: application/json",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/categories/1234",
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
JSONObject category = new JSONObject();

category.put("name", "Updated")
    .put("description", "Category for new campaign");

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");

RequestBody body = RequestBody.create(mediaType, category.toString());
Request request = new Request.Builder()
    .url("https://v8.mailperformance.com/categories/1234")
    .put(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .addHeader("cache-control", "no-cache")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/categories/1234");

var request = new RestRequest(Method.PUT);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    name: "New",
    description: "Category for new campaign"
  });

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>


```json
{
  "id": 1234,
  "name": "Updated",
  "description": "Category for new campaign",
  "creationDate": "2016-06-15T07:54:00Z"
}
```

This endpoint updates a category.

### HTTP Request

`POST https://v8.mailperformance.com/categories/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the category to update

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Category's name
description | string | false | Category's description

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your category ID was not found
409 | Conflict -- A category with this name already exists

## Delete a specific Category

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://v8.mailperformance.com/categories/1234",
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
    .url("https://v8.mailperformance.dev/categories/1234")
    .delete()
    .addHeader("x-key", "YOUR XKEY")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://v8.mailperformance.com/categories/1234");

var request = new RestRequest(Method.DELETE);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

This endpoint delete a specific category.

### HTTP Request

`DELETE https://v8.mailperformance.com/categories/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the category to delete

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your category ID was not found
