# DEPRECATED

#Inbox
Inbox is where you'll find all the expressions your users have tried on Ada that couldn't be matched to an existing response. Authentication is required for all endpoints.

##GET `/inbox/`
Retrieves all the items in your organizations inbox. Returns paginated results.

```json
{
   "results":1,
   "inbox":[
      {
         "_id":"574376980973c487310d8118",
         "body":"How do I change my password?",
         "client_handle":"test",
         "outcomes":[]
      }
   ],
   "page":1
}
```

**URL Arguments**

Parameter | Description | Optionality
--- | --- | ---
`?results` | The number of results you want. Default is 10. | _optional_
`?page` | Which page of results you want | _optional_

**Returned Object**

Key | Type | Description
--- | --- | ---
`results` | `int` | The number of results in this page. Maxes out at your `results` argument or 10 if a `results` parameter was not given.
`inbox` | `list` | A list of inbox item `dict`'s. Could be empty.
`page` | `int` | The page you're on. Iterate over pages until `results` is less than the number of `?results` you requested (or 10 if not specified).

**Example**

```py
requests.get(
  url="https://test.ada.support/api/inbox/",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```

##DELETE `/inbox/{_id}`
Deletes an inbox item forever.

```json
{
   "message":"Deleted 574376980973c487310d8118"
}
```

**Returned Object**

Key | Type | Description
--- | --- | ---
`message` | `str` | A message describing how the operation went.

**Example**

```py
requests.delete(
  url="https://test.ada.support/api/inbox/574376980973c487310d8118",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```

##GET `/inbox/count`
Get the count of items in your organizations' inbox.

```json
{
   "count":1
}
```

**Returned Object**

Key | Type | Description
--- | --- | ---
`count` | `int` | The count of items in your inbox.

**Example**

```py
requests.get(
  url="https://test.ada.support/api/inbox/count",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```
