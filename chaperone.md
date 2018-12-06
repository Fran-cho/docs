# Ada Chaperone

> Chaperone is a small JavaScript application that embeds your **Ada** chat bot into your web page.

![ada animated gif](https://user-images.githubusercontent.com/4740147/47372740-5b5dca80-d6b8-11e8-87e7-1b76d48370d8.gif "Ada Animated Gif")

## Table of Contents
1. [Getting Started](#getting-started)
    - [Turn on your bot](#turn-on-your-bot)
    - [Embed Chaperone script](#embed-chaperone-script)
    - [Instantiate Chaperone](#instantiate-chaperone)
2. [Advanced Setup](#advanced-setup)
    - [Constructor](#constructorclienthandle-options-callback)
    - [Turn on your bot](#turn-on-your-bot)
    - [Turn on your bot](#turn-on-your-bot)
3. [FAQ](#faq)
4. [Versioning](#versioning)
5. [Help](#help)

## Getting Started
Getting started with Ada is easy, just follow the steps below. 

[**You can see a working example here.**](https://jsfiddle.net/c8m8u2y4/175/)

### 1. Turn on your bot
The first step towards adding your Ada Chat Bot to your web page is to turn on the Web Chat integration in your Settings > Platforms page.

### 2. Embed Chaperone script
The next step is to add the Chaperone embed script to your page inside of your `<head>...</head>` block:

```html
<script
  src="https://static.ada.support/embed.f8b282eb.min.js"
  integrity="sha384-A0EOe/GwB+wqNjGniuVFup2J8YuMTrTibM487C3K8qHcQkY4J5Ib2PcV9MIXbnxl"
  crossorigin="anonymous"
  charset="utf-8"
></script>
```

### 3. Instantiate Chaperone
The last step is to instantiate Chaperone with the script below. You should add the script to the bottom of your document (after the `</body>` tag).

```html
...
</body>
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle'); // Replace with your bot handle
</script>
</html>
```

That's it! If you've turned on Web Chat in your settings, you should see a small question-mark button on the bottom right corner of your page which will toggle the Web Chat into and out of view.

## Advanced Setup
Chaperone supports numerous **options** and **methods** to help you customize the look and behaviour of your bot.

### constructor(`clientHandle`, `options`, `callback`)
You can specify three parameters which will dictate how your instance of `AdaChaperone` is created.

Parameter | Type | Description
--- | --- | ---
`clientHandle` | `String` | Your bot's handle
`options` | `Object` | Options to customize the Ada bot. See [Options](#options) below
`callback` | `Function` | Specifies a function to be called after the `<iframe>` is finished being set up

Example:
```html
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
      "parentElement": "myElement",
      "customStyles": "*{color:yellow !important;}",
      "private": true
  }, () => {
      console.log("Callback triggered!");
  });
</script>
</html>
```

### Options
Options are passed to Chaperone as an object in the second parameter of your instantiation call. A full list of available options is provided below:

#### `chatterTokenCallback @type {Function}`
Specifies a callback function to be called when the Chatter has been set. The Chatter token is passed to the callback as an argument.

Example:
```html
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
    "chatterTokenCallback": (chatter) => {
      console.log("Do something with chatter token: ", chatter);
    }
  });
</script>
```

#### `cluster @type {String}`
Specifies the Kubernetes cluster to be used. Unless directed an Ada team member you will not need to change this value.


#### `customStyles @type {String}`
The `customStyles` option can be used to override default styles inside the Web Chat iFrame. The value of the string should be the CSS rule-set you wish to apply inside the iFrame. A list of CSS selectors available for targetting can be found in the table below. 

<aside class="warning">
We do not recommend assigning styles to classes you inspect in the DOM. Class naming is subject to change, and can cause your custom styles to break.
</aside>

Selector | Description
--- | ---
`#message-container` | The outer wrapper, containing the top bar, message list, and input bar
`#ada-close-button` | The button used to close the Web Chat window
`#input-bar` | The bottom wrapper, containg the textarea element, send button, and bottom text
`#message-input` | The textarea inside the input bar, used for use input
`#clear-message` | The button used to clear text from the message-input
`#send-button ` | The button for submitting the user input
`#status-bar` | The bottom text inside the input bar
`#close-info-button` | The button to close the setting modal
`#language-selector` | The language select container
`#language-picker` | The language select element
`#terms-of-service` | The terms of service link
`#privacy` | The privacy link
`#messages-list` | The messages container
`#topBar` | The top bar container above the message list
`#info-button` | The settings modal button
`.g-message` | The base message selector
`.g-message--is-owned-by-user` | The selector for messages from the end user

Example:
```html
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
    "customStyles": "*{font-size: 14px !important;}#message-input{background-color: white; border: 1px solid #c1c1c1;}"
  });
</script>
```

#### `greetingHandle @type {String}`
This can be used to customize the greeting messages that new users see. This is useful for setting page-specific greetings across your app. The `greetingHandle` should correspond to the title of the Answer you would like to use in your Ada dashboard.

Example:
```html
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
    "greetingHandle": "My Answer"
  });
</script>
```

#### `language @type {String}`
Takes in a language code to programatically set the bot language. Languages must first be turned on in the **Settings > Multilingual** page of your dashboard. Language codes follow the [ISO 639-1 language format](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

Example:
```html
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
    "language": "fr" // Set bot to french
  });
</script>
```

#### `mobileOverlay @type {Boolean}`
By default, the Web Chat will open in a new window on mobile devices. If you'd prefer to have it open as an overlay overtop the current window, set this option to `true`.

#### `parentElement @type {String|Object}`
Specifies where to mount the `<iframe>` if the default side drawer is not desired. Accepts the `HTMLNode` or `id` of the desired parent element.

Example:
```html
<body>
  ...
  <div id="custom-iframe"></div>
  ...
</body>
<script type="text/javascript">
  const adaBot = new AdaChaperone('client-handle', {
    "parentElement": document.getElementById("custom-iframe")
  });
</script>
```

#### `private @type {Boolean}`
If set to `true`, this will put Web Chat into "Private" mode. This will cause Web Chat to forget conversation history on refresh. This is effectively the same as setting your Web Chat platform persitence to "Forget After Reload" in the **Settings > Platforms** page of your dashboard.


### Methods
At any time you can tell your `AdaChaperone` instance to do a handful of things. The available methods depend on how you instantiated the `AdaChaperone` instance.

#### `destroy()`
Tears down your Chaperone instance. You must do this if you wish to create a new Chaperone instance.

#### `hide()`
Can be used to programatically close the Web Chat view.

This method cannot be used with the `parentElement` option.


#### `setMetaField(fieldName, value) @param {String} @param {String}`
You can use this method to set meta properties for the Chatter. This can be useful for setting information about your end users. For example, you may wish to track the `email` and `name` for conversation attribution. Once set, this information can be accessed in the email attachment from Handoff Form submissions, or via the Chatter modal in the Conversations view of your Ada dashboard.

Example:
```javascript
adaBot.setMetaField('email', 'joe-schmoe123@gmail.com');
adaBot.setMetaField('name', 'Joe Schmoe');
```

#### `show()`
Can be used to programatically open the Web Chat view. This is useful if you would like to open the Web Chat automatically when the page loads, or when clicking a custom butoon.

This method cannot be used with the `parentElement` option.

Example:
```html
<button onclick="adaBot.show()">Open Chat</button>
```

#### `tellFrameTo(message) @param {String}`
Use this method to manipulate the Web Chat `<iframe>`. Use the table below to see what you can tell the frame to do.

`message` | Description
--- | ---
`focus` | Give window focus to the message input in the `<iframe>`
`blur` | Take window focus away from the message input in the `<iframe>`
`reset` | Resets Chat UI with a new Chatter and history
`deleteHistory` | Clears storage so that a new Chatter will be created upon page refresh

## FAQ


## More
Need some help? Get in touch with us at [help@ada.support](mailto:help@ada.support).
