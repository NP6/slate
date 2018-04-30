#Import

## Get a specific import definition

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/imports/12345",
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
  .url("https://backoffice.mailperformance.com/imports/12345")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/imports/12345");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/imports/12345"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "id": 12345,
  "name": "Import 04-04-2016 10 54",
  "creationDate": "2016-04-04T06:54:00Z",
  "binding": 1234,
  "features": [
    {
      "type": "segmentation",
      "segmentId": 12345,
      "emptyExistingSegment": false
    },
    {
      "type": "duplicate",
      "rules": {
        "ignore": true
      }
    },
    {
      "type": "report",
      "sendFinalReport": true,
      "sendErrorReport": true,
      "contactGuids": [
        "ABCDE0123"
      ],
      "groupIds": []
    },
    {
      "type": "database",
      "updateExisting": true,
      "crushData": true
    }
  ],
  "source": {
    "type": "file",
    "creationDate": "0001-01-01T00:00:00Z",
    "filename": "PlhUx08CxS_import.csv"
  }
}
```

This endpoint retrieves a specific import.

### HTTP Request

`GET https://backoffice.mailperformance.com/imports/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the import to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your import ID was not found

## Create a specific import definition

```php
<?php
$action =  [
    "name"                         => "Manual Import",
    "features"                     => [
        [
            "type"                 => "segmentation",
            "segmentId"            => 1234,
            "emptyExisitingSegment"=> false
        ], [
            "type"                 => "duplicate",
            "rules"                => [
                "ignore"           => true
            ]
        ], [
            "type"                 => "report",
            "sendFinalReport"      => true,
            "sendErrorReport"      => true,
            "contactGuids"         => ["1234ABCD"],
            "groupIds"             => []
        ], [
            "type"                 => "database",
            "updateExisting"       => true,
            "crushData"            => false
        ]
    ],
    "binding"                      => 1234
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Accept: application/vnd.mperf.v8.import.v1+json",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/imports/",
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
  <a href="https://github.com/NP6/CookBook/blob/master/php/Imports/createAutoImports.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/Imports/createAutoImports.php
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/Imports/createManualImportOn2Steps.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/Imports/createManualImportOn2Steps.php
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/php/Imports/createManualImports.php" target="_blank">
    https://github.com/NP6/CookBook/blob/master/php/Imports/createManualImports.php
  </a>
  </p>
</blockquote>

```java
JSONObject firstBind = new JSONObject();
firstBind.put("columnIndex", 0)
    .put("fieldId", 1234);

JSONObject secondBind = new JSONObject();
secondBind.put("columnIndex", 1)
    .put("fieldId", 1234);

JSONObject thirdBind = new JSONObject();
thirdBind.put("columnIndex", 2)
    .put("fieldId", -10);

JSONArray binds = new JSONArray();
binds.put(firstBind)
    .put(secondBind)
    .put(thirdBind);

JSONObject importBinding = new JSONObject();

importBinding.put("name", "Binding file mail contact bis")
    .put("separator", 59)
    .put("startAt", 1)
    .put("binds", binds)
    .put("savedImportFormat", true);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, importBinding.toString());
Request request = new Request.Builder()
    .url("https://backoffice.mailperformance.com/imports/")
    .post(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .addHeader("cache-control", "no-cache")
    .addHeader("Accept", "application/vnd.mperf.v8.import.v1+json")
    .build();

Response response = client.newCall(request).execute();
```

<blockquote class="lang-specific java">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/Imports/createAutoImport.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/Imports/createAutoImports.java
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/Imports/createManualImportOn2Steps.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/Imports/createManualImportOn2Steps.java
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/java/Imports/createManualImports.java" target="_blank">
    https://github.com/NP6/CookBook/blob/master/java/Imports/createManualImports.java
  </a>
  </p>
</blockquote>

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/imports");

var request = new RestRequest(Method.POST);

request.RequestFormat = DataFormat.Json;

request.AddHeader("content-type", "application/json")
    .AddHeader("x-key", "YOUR XKEY")
    .AddHeader("Accept", "application/vnd.mperf.v8.import.v1+json");
request.AddBody(new {
    name: "Manual Import",
    features: [{
        type: "segmentation",
        segmentId: 1234,
        emptyExisitingSegment: false

    }, {
        type: "duplicate",
        rules: {
            ignore: true

        }

    }, {
            type: "report",
            sendFinalReport: true,
            sendErrorReport: true,
            contactGuids: ["1234ABCD"],
            groupIds: []

    }, {
            type: "database",
            updateExisting: true,
            crushData: false

    }],
    binding: 1234
});

IRestResponse response = client.Execute(request);
```

<blockquote class="lang-specific csharp">
  <p>More detail here:
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createAutoImports.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createAutoImports.cs
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createManualImportOn2Steps.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createManualImportOn2Steps.cs
  </a>
  <br />
  <a href="https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createManualImports.cs" target="_blank">
    https://github.com/NP6/CookBook/blob/master/Csharp/Imports/createManualImports.cs
  </a>
  </p>
</blockquote>

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -H "Accept: application/vnd.mperf.v8.import.v1+json"
     -X POST "https://backoffice.mailperformance.com/imports" -d '
{
    "name"                         : "Manual Import",
    "features"                     : [
        {
            "type"                 : "segmentation",
            "segmentId"            : 1234,
            "emptyExisitingSegment": false
        }, {
            "type"                 : "duplicate",
            "rules"                : {
                "ignore"           : true
            }
        }, {
            "type"                 : "report",
            "sendFinalReport"      : true,
            "sendErrorReport"      : true,
            "contactGuids"         : ["1234ABCD"],
            "groupIds"             : []
        }, {
            "type"                 : "database",
            "updateExisting"       : true,
            "crushData"            : false
        }
    ],
    "binding"                      : 1234
}'
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>


```json
{
  "id": 12345,
  "name": "Manual Import",
  "creationDate": "2016-06-13T16:20:43.656Z",
  "binding": 1234,
  "features": [
    {
      "type": "segmentation",
      "segmentId": 12345,
      "emptyExisitingSegment": false
    },
    {
      "type": "duplicate",
      "rules": {
        "ignore": true
      }
    },
    {
      "type": "report",
      "sendFinalReport": true,
      "sendErrorReport": true,
      "contactGuids": [
        "1234ABCD"
      ],
      "groupIds": []
    },
    {
      "type": "database",
      "updateExisting": true,
      "crushData": false
    }
  ],
  "source": {
    "type": "file",
    "creationDate": "2016-06-13T16:20:43.656Z",
    "filename": null
  }
}
```

This endpoint creates an import.

It is imperative to add the Accept request-header field :

`Accept: application/vnd.mperf.v8.import.v1+json`

### HTTP Request

`POST https://backoffice.mailperformance.com/imports/`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Import's name
features | array | false | Array containing all the features of the import
---- type | string | true | Name of the feature
---- segmentId | int | false | Id of the segment that will contain the import
---- emptyExisitingSegment | bool | false | Specify if you want to empty the segment before import or no
---- rules | array | false | Duplicate Rules
-------- ignore | bool | false | Specify if the duplicate will be ignored
---- sendFinalReport | bool | true | Specify if the final report will be sent
---- sendErrorReport | bool | true | Specify if the error report will be sent
---- contactGuids | string[] | true | String array of all contact that will receive import report
---- groupIds | int[] | true | Int array of all groups that will receive import report
---- updateExisting | bool | true | Specify if the existing target will be update with the import
---- crushData | bool | true | Specify if the import will be crush by the data
binding | int | false | Id of the binding to use with the import
scheduler | object | false | Scheduler object for auto import
---- type | string | true | For import automatic : type = "periodic"
---- name | string | true | Scheduler's name
---- frequency | object | true |
-------- occurs | object | true |
------------ type | string | true | Type : "daily" / "weekly" / "monthly"
------------ days | string | false | If type = "weekly" : "days" = "Mon" (exemple) | If type = "Mensuel" : "days" = 2 (exemple)
-------- periodicity | object | false |
------------ type | string | false | Type = "Once"
------------ value | object | false |
---------------- hour | int | false | hour
---------------- minute | int | false | minute
---------------- second | int | false | second
---- validity | object | true |
-------- start | object | true | Date of start of the auto import
---------------- year | int | true | year
---------------- month | int | true | month
---------------- date | int | true | date
---------------- hour | int | true | hour
---------------- minute | int | true | minute
---------------- second | int | true | second
-------- end | object | true | Date of end of the auto import
---------------- year | int | true | year
---------------- month | int | true | month
---------------- date | int | true | date
---------------- hour | int | true | hour
---------------- minute | int | true | minute
---------------- second | int | true | second

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request

## Get a specific import binding

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/importFormats/1234",
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
  .url("https://backoffice.mailperformance.com/importFormats/1234")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/importFormats/1234");

var request = new RestRequest(Method.GET);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/importFormats/1234"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "identifier": {
    "guid": 1234
  },
  "name": "Binding for file n. 42",
  "separator": 59,
  "startAt": 1,
  "binds": [
    {
      "columnIndex": 0,
      "fieldId": -10
    },
    {
      "columnIndex": 1,
      "fieldId": 1234
    },
    {
      "columnIndex": 2,
      "fieldId": 1234
    },
    {
      "columnIndex": 3,
      "fieldId": 1234
    },
    {
      "columnIndex": 4,
      "fieldId": -10
    },
    {
      "columnIndex": 5,
      "fieldId": -10
    }
  ],
  "savedImportFormat": true
}
```

This endpoint retrieves a specific binding.

### HTTP Request

`GET https://backoffice.mailperformance.com/importFormats/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the binding to retrieve

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your import ID was not found

## Create a specific import binding

```php
<?php
$action =  [
    "name"                  => "Binding file mail contact",
    "separator"             => 59,
    "startAt"               => 1,
    "binds"                 => [
        [
            "columnIndex"   => 0,
            "fieldId"       => 1234
        ],
        [
            "columnIndex"   => 1,
            "fieldId"       => 1234
        ],
        [
            "columnIndex"   => 2,
            "fieldId"       => -10
        ]
    ],
    "savedImportFormat"     => true
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "content-type: application/json",
    "x-key: YOUR XKEY",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/importFormats/",
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
JSONObject firstBind = new JSONObject();
firstBind.put("columnIndex", 0)
    .put("fieldId", 1234);

JSONObject secondBind = new JSONObject();
secondBind.put("columnIndex", 1)
    .put("fieldId", 1234);

JSONObject thirdBind = new JSONObject();
thirdBind.put("columnIndex", 2)
    .put("fieldId", -10);

JSONArray binds = new JSONArray();
binds.put(firstBind)
    .put(secondBind)
    .put(thirdBind);

JSONObject mailMessage = new JSONObject();

mailMessage.put("name", "Binding file mail contact bis")
    .put("separator", 59)
    .put("startAt", 1)
    .put("binds", binds)
    .put("savedImportFormat", true);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, mailMessage.toString());
Request request = new Request.Builder()
    .url("https://backoffice.mailperformance.com/importFormats/")
    .post(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .addHeader("cache-control", "no-cache")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/importFormats");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json");
request.AddHeader("x-key", "YOUR XKEY");
request.AddBody(new {
    name = "Binding file mail contact bis",
    separator = 59,
    startAt = 1,
    binds = [
        {
            columnIndex = 0,
            fieldId = 1234
        },
        {
            columnIndex = 1,
            fieldId = 1234
        },
        {
            columnIndex = 2,
            fieldId = -10
        }
    ],
    savedImportFormat = true
});

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -X POST "https://backoffice.mailperformance.com/importFormats" -d '
{
    "name"                  : "Binding file mail contact",
    "separator"             : 59,
    "startAt"               : 1,
    "binds"                 : [
        {
            "columnIndex"   : 0,
            "fieldId"       : 1234
        },
        {
            "columnIndex"   : 1,
            "fieldId"       : 1234
        },
        {
            "columnIndex"   : 2,
            "fieldId"       : -10
        }
    ],
    "savedImportFormat"     : true
}'
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "identifier": {
    "guid": 1234
  },
  "name": "Binding file mail contact",
  "separator": 59,
  "startAt": 1,
  "binds": [
    {
      "columnIndex": 0,
      "fieldId": 1234
    },
    {
      "columnIndex": 1,
      "fieldId": 1234
    },
    {
      "columnIndex": 2,
      "fieldId": -10
    }
  ],
  "savedImportFormat": true
}
```

This endpoint create a new Binding.

### HTTP Request

`POST https://backoffice.mailperformance.com/importFormats`

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
name | string | true | Binding's name
separator | int | true | ASCII value of the separator
startAt | int | true | Value of start
binds | array | true | Array containing all the bindings
---- columnIndex | int | true | Position of the column
---- fieldId | int | true | Id corresponding to the column
savedImportFormat | bool | true | Specify if the binding will be safe

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
409 | Conflict -- A import binding with this name already exists

## Associate a source to a specific import

```php
<?php
$fileContent = "nom;prenom;email;\nDupont;Jean;JD@test.com";

$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY",
    "content-type: application/octet-stream",
    "Accept: application/vnd.mperf.v8.import.v1+json",
    "content-disposition: form-data; filename=filename.csv"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/imports/12345/source",
    CURLOPT_CUSTOMREQUEST   => "PUT",
    CURLOPT_HTTP_VERSION    => CURL_HTTP_VERSION_1_1,
    CURLOPT_RETURNTRANSFER  => true,
    CURLOPT_TIMEOUT         => 30,
    CURLOPT_HTTPHEADER      => $httpHeader,
    CURLOPT_POSTFIELDS      => $fileContent
];

curl_setopt_array($curl, $opts);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);
?>
```

```java
String fileContent = "nom;prenom;email;\nDupont;Jean;JD@test.com";

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/octet-stream");

RequestBody body = RequestBody.create(mediaType, fileContent);

Request request = new Request.Builder()
  .url("https://backoffice.mailperformance.com/imports/12345/source")
  .put(body)
  .addHeader("x-key", "YOUR XKEY")
  .addHeader("content-disposition", "form-data; filename=filename.csv")
  .addHeader("content-type", "application/octet-stream")
  .addHeader("Accept", "application/vnd.mperf.v8.import.v1+json")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var fileContent = "nom;prenom;email;\nDupont;Jean;JD@test.com";

var client = new RestClient("https://backoffice.mailperformance.com/imports/12345/source");

var request = new RestRequest(Method.PUT);

request.AddHeader("content-type", "application/octet-stream")
    .AddHeader("content-disposition", "form-data; filename=filename.csv")
    .AddHeader("x-key", "YOUR XKEY")
    .AddHeader("Accept", "application/vnd.mperf.v8.import.v1+json");

request.AddParameter("application/octet-stream", fileContent, ParameterType.RequestBody);

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/octet-stream"
     -H "Content-disposition: form-data; filename=filename.csv"
     -H "Accept: application/vnd.mperf.v8.import.v1+json"
     -X PUT "https://backoffice.mailperformance.com/imports/12345/source"
     -d 'nom;prenom;email;\nDupont;Jean;JD@test.com'
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
  "type": "file",
  "creationDate": "0001-01-01T00:00:00Z",
  "updateDate": "2016-06-14T15:03:24.788Z",
  "filename": "3ec15c5168_filename.csv"
}
```

This endpoint associate a source file to an import.

It is imperative to add the Accept request-header field :

`Accept: application/vnd.mperf.v8.import.v1+json`

### HTTP Request

`PUT https://backoffice.mailperformance.com/imports/<ID>/source`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the import to update

### Query Parameters

You will send a String that is the content of the file.

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not found -- Your import ID was not found

## Execute a specific import

```php
<?php
$action = [
    "binding"                  => 1234
];

$data = json_encode($action);

$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY",
    "content-type: application/json",
    "Accept: application/vnd.mperf.v8.import.v1+json",
    "Content-Length: " . strlen($data)
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/imports/12345/executions",
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
JSONObject imports = new JSONObject();
imports.put("binding", 1234);

OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");

RequestBody body = RequestBody.create(mediaType, imports.toString());

Request request = new Request.Builder()
    .url("https://backoffice.mailperformance.com/imports/12345/executions")
    .post(body)
    .addHeader("x-key", "YOUR XKEY")
    .addHeader("content-type", "application/json")
    .addHeader("cache-control", "no-cache")
    .addHeader("Accept", "application/vnd.mperf.v8.import.v1+json")
    .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/imports/12345/executions");

var request = new RestRequest(Method.POST);

request.AddHeader("content-type", "application/json")
    .AddHeader("x-key", "YOUR XKEY")
    .AddHeader("Accept", "application/vnd.mperf.v8.import.v1+json");
request.AddBody(new {
    binding = 1234
});

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" -H "Content-Type: application/json"
     -H "Accept: application/vnd.mperf.v8.import.v1+json"
     -X POST "https://backoffice.mailperformance.com/imports/12345/executions"
     -d '{ "binding": 1234 }'
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json
{
	"startDate": "2016-06-14T15:49:48.568Z",
	"state": 0,
	"content": {
		"features": [{
			"type": "report",
			"sendFinalReport": true,
			"sendErrorReport": true,
			"contactGuids": [
				"1234ABCD"
			],
			"groupIds": []
		}, {
			"type": "database",
			"updateExisting": true,
			"crushData": false
		}],
		"identifier": {
			"guid": 1234
		},
		"name": "Binding file mail contact",
		"separator": 59,
		"startAt": 1,
		"binds": [{
			"columnIndex": 0,
			"fieldId": 1234
		}, {
			"columnIndex": 1,
			"fieldId": 1234
		}, {
			"columnIndex": 2,
			"fieldId": -10
		}],
		"savedImportFormat": true
	},
	"source": {
		"type": "file",
		"creationDate": "0001-01-01T00:00:00Z",
		"updateDate": "2016-06-14T15:03:24.788Z",
		"filename": "3ec15c5168_filename.csv"
	}

}
```

This endpoint start a new execution for an import.

It is imperative to add the Accept request-header field :

`Accept: application/vnd.mperf.v8.import.v1+json`

### HTTP Request

`POST https://backoffice.mailperformance.com/imports/<ID>/executions`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the import to execute

### Query Parameters

Property | Type | Required | Description
-------- | ---- | -------- | -----------
binding | int | true | Id of the binding to use with the import
features | array | false | Array containing all the features of the import
---- type | string | true | Name of the feature
---- segmentId | int | false | Id of the segment that will contain the import
---- emptyExisitingSegment | bool | false | Specify if you want to empty the segment before import or no
---- rules | array | false | Duplicate Rules
-------- ignore | bool | false | Specify if the duplicate will be ignored
---- sendFinalReport | bool | true | Specify if the final report will be sent
---- sendErrorReport | bool | true | Specify if the error report will be sent
---- contactGuids | string[] | true | String array of all contact that will receive import report
---- groupIds | int[] | true | Int array of all groups that will receive import report
---- updateExisting | bool | true | Specify if the existing target will be update with the import
---- crushData | bool | true | Specify if the import will be crush the data

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
