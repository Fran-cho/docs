#Messages
The messages endpoint is where you can create new messages for Ada to respond to.

##POST `/message`
Creates a new message for ada to respond to based on your message object. The formatting of your object depends on the platform you're using. Below are documentation for bots using our HTTP API integration.

**Expected Keys**

Parameter | Description | Optionality
--- | --- | ---
`by` | A unique name for your user who created the message | **needed**
`body` | A string of text which represents the value of the message type | **needed**
`external_message_id` | An ID that corresponds to the message in your datastore | _optional_
`external_chat_id` | An ID that corresponds to the conversation in your datastore | _optional_
`type` | The type of message you're sending. Can be either `text` or `trigger` | _optional_ (Default is `text`)

**Message Types**

Type | Description
--- | ---
`text` | A basic text message from a user to your bot. The `body` should be something like `"Hey Ada, how do I change my password?"`
`trigger` | Sent when a user has pressed a button. The `body` of your message should be a `response_id` corresponding to the response you want us to send back to you.


**Example Text Message**
```json
{  
  "by" : "davidhariri",
  "body" : "Hey Ada, how do I change my password?",
  "external_message_id" : "1234",
  "external_chat_id" : "5678",
}
```

**Example Trigger Message**
```json
{  
  "by" : "davidhariri",
  "body" : "5754x77x8c8d355ee1d44753",
  "external_message_id" : "1234",
  "external_chat_id" : "5678",
  "type" : "trigger"
}
```

**Example Response**
```
200, "{message : "Message Processing"}"
```

After queueing and processing your message we will ping your servers back at the URL you specified in your HTTP web hook with a response object. To keep track of inbound messages and who they should route to in your application you should give each of your conversations a unique identifier and make use of the `external_chat_id` field. We aim to always complete these requests in 300ms or less.

**Example Response Object**
```
{
  "to" : "davidhariri",
  "external_message_id" : "1234",
  "external_chat_id" : "5678",
  "messages" : [
    {
      "type" : "text",
      "body" : "To change your password, follow these instructions:",
      "index" : 0
    },
    {
      "type" : "link",
      "title" : "Change Password Instructions",
      "url" : "https://ada.zendesk.com/kb/change-password.html",
      "index" : 1
    },
    {
      "type" : "text",
      "body" : "Did that help?",
      "index" : 2
    }
  ],
  "suggested_responses" : [
    {
      "type" : "text",
      "body" : "Yes",
      "response_id" : "5754x77x8c8d355ee1d44753"
    },
    {
      "type" : "text",
      "body" : "No",
      "response_id" : "5754x77x8c8dy5pee1d44754"
    }
  ]
}
```
