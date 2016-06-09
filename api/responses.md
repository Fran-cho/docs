#Responses

##POST `/responses/`
This endpoint creates a new response object for your bot to use to respond to messages.

**Expected Keys**

Parameter | Description | Optionality
--- | --- | ---
`handle` | A unique name for your response. We encourage you to make this short and descriptive. | **needed**
`button_label` | A string of text which represents how this response will be included as a button in other responses | _optional_
`messages` | A list of messages to be sent back when this response is triggered | **need at least 1**
`options` | A list of response `_id`'s to be included as suggested responses (as buttons, hints etc...) | _optional_

**Example**
```json
{  
  "handle" : "My test response",
  "button_label" : "Test Me",
  "messages" : [
    {
      "type" : "text",
      "body" : "You tested me!"
    }
  ]
}
```

**Example Response**
`201:Created`
```
{  
  "_id" : "573f068174efb80a55dbdeb8",
  "handle" : "My test response",
  "closer" : false,
  "rating" : null,
  "button_label" : "Test Me",
  "messages" : [
    {
      "type" : "text",
      "body" : "You tested me!"
    }
  ],
  "options" : []
}
```
