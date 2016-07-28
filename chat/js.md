#JavaScript API
The JavaScript API was created for two reasons:

1. For making it possible to include an Ada chat window easily and seemlessly across your entire web presence.
2. For making it easy to create your own `<iframe>`'s, but still maintaining the ability to perform key manipulations with the chat window

##Install
To install the Ada JavaScript API on your page add the following to your `<head>`

```html
<script src="https://ada.support/chat/static/js/chaperone.js" charset="utf-8"></script>
```

Next, initialize Ada with your bot's handle:

```html
  ...
  </body>
  <script type="text/javascript">
      Ada.init("acme");
  </script>
</html>
```
*Note:* If you aren't sure what your bot's handle is, it's the first part of the url for the application. So if you manage your bot at `acme.ada.support/app/` then your handle would be `acme`.

##Customize
Initializing with one parameter like the above example will create a button at the bottom right of your website.

###Color
* To tint/colorize the chat UI and the button to your companies liking, add a color in the settings view in the bot management application.
* To change the `<title>` element of the chat window

If it doesn't, please check your console for errors. If there are no errors, it may not show up because you haven't turned on Web Chat in your settings. Please go to your manegement app (https://acme.ada.support/app/) and turn on Web Chat in the settings view.

###API
