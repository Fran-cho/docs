Our API is available to any of our organizations at `{orgname}.ada.support/api/` and expects JSON. The Ada API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like [HTTP authentication](authentication.md) and HTTP verbs, which are understood by off-the-shelf HTTP clients. JSON is returned by all API responses, including errors.

The API is still in beta so you may encounter bugs or things that don't make sense. Please let us know about these by email or in Slack. Thanks!

#Contents

##General
###[Authentication](authentication.md)
###[Errors](errors.md)

##Resources
###[Messages](messages.md)
###[Responses](responses.md)
###[Inbox](inbox.md)
###[Users](users.md)

## Response Codes
We use standard HTTP status codes in our responses to notify you of how things went with your requests.

Code | Description
--- | ---
**200** | Your `GET` request was successful and the resource was returned to you. Your `POST` request was successful and the modified resource was returned to you. Your `DELETE` operation was successful.
**201** | Your `POST` request was successful and a new resource was returned to you.
**400** | Your request was malformed and could not be executed.
**401** | Your request did not include a proper authentication header.
**403** | You included an authorization header, but you're not authorized to access the requested resource.
**404** | We couldn't find the resource you requested.
**405** | You're accessing an endpoint with a method that isn't supported.
**500** | Your request made our server explode :fire:. Report it [in issues](https://github.com/AdaSupport/api/issues)!

## Settings
At the moment, there is no way to modify your settings through the app or the API. Please do this manually by pinging @david in Slack for now. _(We're working on it...)_

## Endpoints
### /
Method | Auth? | Description
--- | --- | --- 
**GET** | Required | Use this endpoint to test your API authentication

### /message/
Messages are how Ada communicates with the world. She accepts messages in the form of text and sends back link, picture, video and text messages. You can specify the type of response Ada should send back to your app inside of _our_ app when you make and train new responses.

Method | Auth? | Description
--- | --- | --- 
**POST** | None | Used to send Ada messages. Must specify a `?key={YOUR-KEY}` parameter which we can use to validate your requests. Talk to @david in Slack for now about setting this.

**Message Request**
```js
{
  "by" : "davidhariri", // Who the message is from. This is a unique identifier which you specify and use to direct the response we make back to the user who made the message
  "body" : "What is a Giraffe? 😊", // What the user is asking. Full UTF-8 support including Emoji.
  "external_message_id" : "1234",//*Optionally* identify your users' message. We'll pass back this id with our response to you if you specify it.
  "external_chat_id" : "5678",// *Optionally* identify your users' chat (if you support multiple chats for each user). We'll pass back this id with our response to you if you specify it.
}
```

**Message Response**

Once your message to us has been processed (asynchronously) we'll send back a response to the url specified in your integration settings as a `POST` request. This will include one of these objects (depending on how you configured your response in Ada's app):

```js
// Our response object to your hook URL will include a list of messages in response to the original message from your user
{
  "to" : "davidhariri",
  "external_message_id" : "1234",
  "external_chat_id" : "5678",
  "messages" : [
    {
      "type" : "text",
      "body" : "Hello there!"
    },
    {
      "type" : "link",
      "body" : "Here's an interesting article",
      "url" : "http://giraffefacts.org/facts.html",
      "pic_url" : "http://giraffefacts.org/facts.html"
    },
    {
      "type" : "picture",
      "pic_url" : "http://giraffefacts.org/eating.jpg"
    },
    {
      "type" : "video",
      "vid_url" : "http://giraffefacts.org/walking.mp4"
    }
  ],
  "suggested_responses" : [
    "Thanks, that helped!",
    "That doesn't help..."
  ]
}
```
