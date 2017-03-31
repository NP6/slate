#Conversations

## Get conversation by id

```php
<?php
$curl = curl_init();

$httpHeader = [
    "x-key: YOUR XKEY"
];

$opts = [
    CURLOPT_URL             => "https://backoffice.mailperformance.com/messages/<CONVERSATION_ID>",
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
  .url("https://backoffice.mailperformance.com/messages/<CONVERSATION_ID>")
  .get()
  .addHeader("x-key", "YOUR XKEY")
  .build();

Response response = client.newCall(request).execute();
```

```csharp
var client = new RestClient("https://backoffice.mailperformance.com/messages/<CONVERSATION_ID>");

var request = new RestRequest(Method.GET);

request.AddHeader("x-key", "YOUR XKEY");

IRestResponse response = client.Execute(request);
```

```shell
curl -H "X-Key: YOUR XKEY" "https://backoffice.mailperformance.com/messages/<CONVERSATION_ID>"
```

<blockquote class="lang-specific json">
  <p>The request returns a JSON structured like this: </p>
</blockquote>

```json

{ 
    "type" : "message", 
    "media" : "mail", 
    "id" : "6dc5cd3d-e233-4359-be70-088833f89bff", 
    "actionId" : "000JKG", 
    "target" : "000QE6KY", 
    "events" : [
        { "type" : "requested", "date" : "2017-03-31T07:48:16.378Z" },
        { "type" : "received", "origin" : "smtp", "date" : "2017-03-31T07:48:20Z", "recipient" : "xxx@yyy.com" }
    ] 
}

```

This endpoint retrieves all the conversation events for a specific conversation.

### HTTP Request

`GET https://backoffice.mailperformance.com/messages/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the conversation to retrieve

### Conversation types
Name | Description
---- | -----------
requested | The message has been handled by the platform
received | The smtp server has sent the message
bounced | The message has bounced
canceled | The message has been canceled before be sent to the smtp server (ex: an error has occured during the rendering of the mail)

### Return Codes

Code | Description
---- | -----------
200 | Success -- OK
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- Your conversation ID was not found
