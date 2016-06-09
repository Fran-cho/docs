#Messages
The messages endpoint is where you can create new messages for Ada to respond to.

##POST `/message`
Creates a new message for ada to respond to based on your message object. The formatting of your object depends on the platform you're using. Below are documentation for bots using our HTTP API integration.

**Expected Keys**

Parameter | Description | Optionality
--- | --- | ---
`by` | A unique name for your user who created the message | **needed**
`body` | A string of text which represents the users message | **needed**
`external_message_id` | An ID that corresponds to the message in your datastore | _optional_
`external_chat_id` | An ID that corresponds to the conversation in your datastore | _optional_

**Example**
```json
{  
  "by" : "davidhariri",
  "body" : "test",
  "external_message_id" : "1234",
  "external_chat_id" : "5678",
}
```

**Example Response**
```
201, "{message : "Message Processing"}"
```

After this, we will ping your servers back at the URL you specified in your HTTP web hook with our response object. This typically happens within 300ms.
