# Errors

The NP6 API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your json is probably wrong
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- You don't have permission for this request
404 | Not Found -- The specified resource could not be found
409 | Conflict -- This resource already exists
410 | Gone -- The resource requested has been removed from our servers
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily  offline for maintenance. Please try again later.
