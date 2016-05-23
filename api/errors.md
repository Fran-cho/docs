##Errors
We use standard HTTP status codes in our responses to notify you of how things went with your requests. If something went wrong, an error will be returned formatted as JSON with a `message` in most cases. It will look something like this:

```
{
  "message" : "Missing 'body' parameter"
}
```

##Codes
Code | Description
--- | ---
**200** | Your `GET` request was successful and the resource was returned to you. Your `POST` request was successful and the modified resource was returned to you. Your `DELETE` operation was successful.
**201** | Your `POST` request was successful and a new resource was returned to you.
**400** | Your request was malformed and could not be executed. Check the returned message for more information.
**401** | Your request did not include a proper authentication header.
**403** | You included an authorization header, but you're not authorized to access the requested resource.
**404** | We couldn't find the resource you requested.
**405** | You're accessing an endpoint with a method that isn't supported.
**500** | Nice, your request made our server explode :fire:
