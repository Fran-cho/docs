#JavaScript API
The JavaScript API was created for two reasons:

1. For making it possible to include an Ada chat window easily and seemlessly across your entire web presence.
2. For making it easy to create your own `<iframe>`'s, but still maintaining the ability to perform key manipulations with the chat window

##Install
To install the Ada JavaScript API on your website, add the following to the `<head>...</head>` block of your page:

```html
<script src="https://ada.support/chat/static/js/chaperone.js" charset="utf-8"></script>
```

Next, initialize Ada with your bot's handle near the bottom of your page:

```html
  ...
  </body>
  <script type="text/javascript">
      Ada.init("acme");
  </script>
</html>
```
*Note:* If you aren't sure what your bot's handle is, it's the first part of the url for the application. So if you manage your bot at `https://acme.ada.support/app/` then your handle would be `acme`.

###Callback
You can have the script fire a callback once it's done initializing the chat session like so:

```html
  </body>
  <script type="text/javascript">
      Ada.init("acme", undefined, function() {
        // Clear the old conversation from the conversation history
        Ada.tellFrameTo("reset");
      });
  </script>
</html>
```

##Customize
Initializing with one parameter like the above example will create a button at the bottom right of your website.

###Location
If you'd like to put the chat window in a specific element on your page, you can include a second parameter which should be an `id` to an element on the page which you'd like to be the parent of the `<iframe>`:

```html
  ...
  </body>
  <script type="text/javascript">
      Ada.init("acme", "some-chat-element");
  </script>
</html>
```

###Color
* To tint/colorize the chat UI and the button to your companies liking, add a valid HTML color value (ex. `#22d9ba`, `red`) in the settings view under General > Color in your bot management application (https://acme.ada.support/app/).
* To change the `<title>` element of the chat window specify a "Name" in the same area as the color.

##Troubleshooting
If it doesn't, please check your console for errors. If there are no errors, it may not show up because you haven't turned on Web Chat in your settings. Please go to your manegement app (https://acme.ada.support/app/) and turn on Web Chat in the settings view.

##API
The following methods are exposed under the `Ada` namespace on your page:

Method | Description | Acceptable Values
--- | --- | ---
`Ada.chatWindow.show()` | Shows the chat window | _None_
`Ada.chatWindow.hide()` | Hides the chat window | _None_
`Ada.tellFrameTo(String)` | Asks the chat window to do something | `reset`, `blur`, `focus`
