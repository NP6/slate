#Field

## Get all Field

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/fields/",
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
  .url("https://backoffice.mailperformance.com/fields/")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/fields/");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The response from the API is an array structured like this:</p>
</blockquote>

```json
[
  {
    "type": "email",
    "id": 12345,
    "name": "Email",
    "isUnicity": true,
    "isMandatory": true
  },
  {
    "type": "textField",
    "id": 12346,
    "name": "Name",
    "isUnicity": false,
    "isMandatory": true
  }
]
```

This endpoint retrieves all fields.

### HTTP Request

`GET https://backoffice.mailperformance.com/actions`

### Query Parameters

None

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific Field

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/fields/12345",
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
  .url("https://backoffice.mailperformance.com/fields/12345")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/fields/12345");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The response from the API is a json structured like this:</p>
</blockquote>

```json
  {
    "type": "email",
    "id": 12345,
    "name": "Email",
    "isUnicity": true,
    "isMandatory": true
  }
```

This endpoint retrieves a specific field.

### HTTP Request

`GET https://backoffice.mailperformance.com/fields/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the field to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your field ID was not found

## Create a Field

```php
<?php
$field =  [
  "type"        => "textField",
  "name"        => "Firstname",
  "isUnicity"   => false,
  "isMandatory" => false,
  "constraint"  => [
    "operator"    => 4,
    "value"       => "150"
  ]
];

$data = json_encode($field);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/fields/",
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
  <a href="https://github.com/NP6/CookBook/blob/master/php/createField.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/createField.php
  </a>
  </p>
</blockquote>

```java
JSONObject json = new JSONObject();
JSONObject constraint = new JSONObject();

constraint.put("operator", 4)
          .put("value", "150");

json.put("type", "textField")
    .put("name", "Firstname")
    .put("isUnicity", false)
    .put("isMandatory", false)
    .put("constraint", constraint);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/fields/")
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
  <a href="https://github.com/NP6/CookBook/blob/master/java/createField.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/createField.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/fields/");

var request = new RestRequest(Method.POST);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
  type = "textField",
  name = "Firstname",
  isUnicity = false,
  isMandatory = false
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/createField.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/createField.cs
  </a>
  </p>
</blockquote>

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "type": "singleSelectList",
  "id": 12347,
  "name": "civility",
  "isUnicity": false,
  "isMandatory": false,
  "constraint": {     //optional
    "operator": 4,
    "value": "150"
  },
  "valueListId": 1234 //only for singleSelectList and multipleSelectList
}
```

This endpoint creates a field.

### HTTP Request

`POST https://backoffice.mailperformance.com/fields`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Field's type ['singleSelectList', 'multipleSelectList', 'email', 'phone', 'textArea', 'numeric', 'textField' or 'date']
name | string | true | Field's name
isUnicity | boolean | true | True if used for unicity, no otherwise
isMandatory | boolean | true | True if the field is mandatory, no otherwise
constraint | object | false | Define a contraint for this field
---- operaor | int | false | Constraint operator
---- value | string | false | Constraint value
valueListId | int | false | The id of the associated value list

### Constraint operator list

Value | Operator
----- | --------
0 | None
1 | Greater than
2 | Smaller than
3 | Greater than or equal
4 | Smaller than or equal
5 | Equal

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict -- A field with this name already exists

## Update a specific Field

```php
<?php
$field =  [
  "type"        => "textField",
  "name"        => "Firstname",
  "isUnicity"   => false,
  "isMandatory" => false,
  "constraint"  => [
    "operator"    => 4,
    "value"       => "150"
  ]
];

$data = json_encode($field);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/fields/12345",
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
JSONObject constraint = new JSONObject();

constraint.put("operator", 4)
          .put("value", "150");

json.put("type", "textField")
    .put("name", "Firstname")
    .put("isUnicity", false)
    .put("isMandatory", false)
    .put("constraint", constraint);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, json.toString());
Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/fields/12345")
  .put(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-type", "application/json")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/fields/12345");

var request = new RestRequest(Method.PUT);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
  type = "textField",
  name = "Firstname",
  isUnicity = false,
  isMandatory = false
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "type": "singleSelectList",
  "id": 12347,
  "name": "civility",
  "isUnicity": false,
  "isMandatory": false,
  "constraint": {     //optional
    "operator": 4,
    "value": "150"
  },
  "valueListId": 1234 //only for singleSelectList and multipleSelectList
}
```

This endpoint updates a specific field.

### HTTP Request

`PUT https://backoffice.mailperformance.com/fields/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the field to update

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
type | string | true | Field's type ['singleSelectList', 'multipleSelectList', 'email', 'phone', 'textArea', 'numeric', 'textField' or 'date']
name | string | true | Field's name
isUnicity | boolean | true | True if used for unicity, no otherwise
isMandatory | boolean | true | True if the field is mandatory, no otherwise
constraint | object | false | Define a contraint for this field
---- operaor | int | false | Constraint operator
---- value | string | false | Constraint value
valueListId | int | false | The id of the associated value list

### Constraint operator list

Value | Operator
----- | --------
0 | None
1 | Greater than
2 | Smaller than
3 | Greater than or equal
4 | Smaller than or equal
5 | Equal

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your field ID was not found
409 | Conflict -- A field with this name already exists

## Delete a specific Field

```php
<?php
$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/fields/12345",
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
```

```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/fields/12345")
  .delete()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/fields/12345");

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

This endpoint deletes a specific field.

### HTTP Request

`DELETE https://backoffice.mailperformance.com/fields/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the field to delete

### Return Codes

Code | Description
---- | -----------
204 | Success -- No content
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your field ID was not found
