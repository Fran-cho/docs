# Chaperone

[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

> Chaperone is a small JavaScript application that embeds your **Ada** chat bot into your web page.

## Getting Started
#### Turn on your bot
The first step towards adding your Ada chat bot to your web page is to turn on the Web Chat integration in your Settings > Platforms page. 

#### Embed Chaperone script
The next step is to add the Chaperone embed script to your page inside of your `<head>...</head>` block:

```html
<script src="https://static.ada.support/embed.fef7a3d4.min.js" charset="utf-8"></script>
```

#### Instantiate Chaperone
The last step is to instantiate Chaperone with the script below. You should add the script to the bottom of your document (after the `</body>` tag).

```html
</body>
<script type="text/javascript">
    const adaBot = new AdaChaperone('client-handle'); // Replace with you bot handle
</script>
</html>
```

That's it! If you've turned on Web Chat in your settings, you should see a small question-mark button on the bottom right corner of your page which will toggle the Web Chat into and out of view.

## Advanced Set Up
Chaperone can accept various options and methods that will help to customize the look and behaviour of your bot. 

### constructor(`clientHandle`, `options`, `callback`)
You can specify three parameters which will dictate how your instance of `AdaChaperone` is created. 

Parameter | Types | Description
--- | --- | ---
`clientHandle` | `String` | This should be your bot's handle (your handle is **this**[.ada.suport/app])
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

Name  | Type | Default | Description
--- | --- | --- | ---
`parentElement` | `String` or `Object` | `null` | Specifies where to build the `<iframe>` if the default side window is not desired. Accepts the `HTMLNode` or `id` of the desired parent element
`customStyles` | `String` | `null` | Takes a string value which can be used to override default styles in the Chat iFrame
`private` | `Boolean` | `false` | If set to `true`, will create a new private instance of the Chat iFrame
`mobileOverlay` | `Boolean` | `false` | By default, the Ada chat will open in a new window on mobile devices. If you'd prefer to have it open as an overlay on the current window, set this option to `true`
`greetingHandle` | `Boolean` | `null` | Customize the greeting message that the user sees by passing in the handle of the response you'd like to use
`chatterTokenCallback` | `Function` | `null` | Specifies a callback function to be called when the Chatter has been set. The Chatter token is passed to the callback as an argument
`cluster` | `String` | `null` | Specifies the cluster to be used


### Methods
At any time in your application you can tell your `AdaChaperone` instance to do a handful of things. The available methods depend on how you instantiated the `AdaChaperone` instance.

#### show()
If you didn't specify a custom element to be the parent element of the `<iframe>`, then this method will show the Web Chat view.

#### hide()
If you didn't specify a custom element to be the parent element of the `<iframe>`, then this method will hide the Web Chat view.

#### destroy()
Tears down your Chaperone instance. You must do this if you wish to create a new Chaperone instance.

#### setMetaField(`str`, `object`)
You can use this method to set locally stored meta properties for the chatter. This is useful in combination with your Handoff Form as any meta data fields you set with this method will be carried through in the email attachment from the form submission so you could see, for example, a `user_id` of the person who created the ticket. See your Settings > Integrations view in your bot manager for more information on Handoff forms.

#### tellFrameTo(`message`)
Use this method to manipulate the chat `<iframe>` inside of the parent element on your page. Use the table below to see what you can tell the frame to do. All `message` values should be of type `String`.

`message` | Description
--- | ---
`focus` | Give window focus to the message input in the `<iframe>`
`blur` | Take window focus away from the message input in the `<iframe>`


