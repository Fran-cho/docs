#Inbox
Inbox is where you'll find all the expressions your users have tried on Ada that couldn't be matched to an existing response.

##/inbox/

**Allowed Verbs**

Verb | Description
--- | ---
**GET** | Retrieves all the items in your organizations inbox. Returns paginated results.


**Returned Fields**

Field | Description
--- | ---
`results` | Integer. The number of results in this page. Maxes out at your `results` argument or 10 if a `results` parameter was not given.
`inbox` | List. A list of inbox items. Can be empty.
`page` | Integer. The page you're on. Iterate over pages until results is less than the number of results you requested (or 10 if not specified).

**URL Arguments**

Parameter | Description | Optionality
--- | --- | ---
`?results` | The number of results you want. Default is 10. | _optional_
`?page` | Which page of results you want | _optional_

**Example**

```py
requests.get(
  url="https://test.ada.support/api/inbox/",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```

**Yields**

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

##/inbox/{item._id}

**Allowed Verbs**

Verb | Description
--- | ---
**DELETE** | Deletes an inbox item based on it's `_id` property.


**Returned Fields**

Field | Description
--- | ---
`message` | String. A message describing how the operation went.

**Example**

```py
requests.get(
  url="https://test.ada.support/api/inbox/",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```

**Yields**

```json
{  
   "message":"Deleted 574376980973c487310d8118"
}
```

##/inbox/count

**Allowed Verbs**

Verb | Description
--- | ---
**GET** | Retrieves the number of unread inbox items you have.

**Returned Fields**

Field | Type
--- | ---
`count` | Integer. The number of inbox items available for the organization tied to your user.

**Example**

```py
requests.get(
  url="https://test.ada.support/api/inbox/count",
  auth=("david", "36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80")
)
```

**Yields**

```json
{  
   "count":1
}
```


