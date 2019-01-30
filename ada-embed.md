# Ada Embed ✨New✨

> Ada Embed is a small JavaScript application that embeds your **Ada** Chat bot into your web page.

![ada animated gif](https://user-images.githubusercontent.com/4740147/47372740-5b5dca80-d6b8-11e8-87e7-1b76d48370d8.gif "Ada Animated Gif")

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Quick Start](#quick-start)
    - [Turn on your bot](#1-turn-on-your-bot)
    - [Embed Chaperone script](#2-embed-chaperone-script)
    - [Instantiate Chaperone](#3-instantiate-chaperone)
3. [Configuring Your Bot](#configuring-your-bot)
    - [Options](#options)
    - [Methods](#methods)
4. [FAQ](#faq)
5. [Versioning](#versioning)
6. [Questions](#questions)

## Prerequisites
This document is intended for bot specialists and developers with working knowledge of HTML. For some of the advanced setup, basic knowledge of JavaScript is required. The document also assumes you have a hosted web page that you have write access to.

## Getting Started
Getting started with Ada is easy, just follow the steps below.

### 1. Turn on your bot
The first step towards adding your Ada Chat Bot to your web page is to turn on the Web Chat integration in your **Settings > Platforms** page.

<img width="600" alt="Ada Dashboard Chat Settings" src="https://user-images.githubusercontent.com/9045634/49764964-f2013d80-fc9e-11e8-8e8e-52ed7774b3bf.png">

### 2. Quick Start
Once you have your website all ready-to-go, find the page where you'd like to embed the Ada Chat bot. This will be a `.html` file (or equivalent). Here you will need to paste the following into the `<head>...</head>` block. Be sure to replace the example data-handle with your own.

```html
<script 
  async 
  id="__ada" 
  data-handle="ada-example"
  src="https://static.ada.support/embed.js"
></script>
```

That's it! You should now see a small question mark button on the bottom right corner of your page. Clicking the button will toggle the Web Chat in and out of view.

[**You can see a working example here.**](https://jsfiddle.net/vr87utse/)

## Configuring Your Bot
Ada Embed supports numerous [settings](#settings) and [actions](#actions) to help you customize the look and behaviour of your bot. Settings are set in the `adaSettings` object when you [embed your script](#2-embed-script). They determine intrinsic properties like bot style and behaviour. Conversely, actions can be called at any point in time to toggle Chat, update user meta data, and more.

### Settings
Settings are set on the window object as `window.adaSettings = {}`. A full list of available settings is provided below:

#### `adaReadyCallback` `@type {Function}`
Specifies a callback function to be called when the Embed script has finished setting up. This is especially useful when Embed is loaded `asynchronously`. 

**Example:**
```html
<script type="text/javascript">
  window.adaSettings = {
    adaReadyCallback: () => {
      console.log("Ada Embed is done setting up. Chat support is now available.");
    },
    ... // The rest of your settings here
  }
</script>
```

#### `chatterTokenCallback` `@type {Function}`
Specifies a callback function to be called when the Chatter has been set. The Chatter token is passed to the callback as an argument.

**Example:**
```html
<script type="text/javascript">
  window.adaSettings = {
    chatterTokenCallback: (chatter) => {
      console.log("Do something with chatter token: ", chatter);
    },
    ... // The rest of your settings here
  }
</script>
```

#### `cluster` `@type {String}`
Specifies the Kubernetes cluster to be used. Unless directed by an Ada team member, you will not need to change this value.


#### `customStyles` `@type {String}`
The `customStyles` option can be used to override default styles inside the Web Chat iFrame. The value of the string should be the CSS rule-set you wish to apply inside the iFrame. A list of CSS selectors available for targetting can be found in the table below.

| WARNING: We do not recommend assigning styles to classes you inspect in the DOM. Class naming is subject to change, and can cause your custom styles to break. |
| --- |

Selector | Description
--- | ---
`#message-container` | The outer wrapper, containing the top bar, message list, and input bar
`#ada-close-button` | The button used to close the Web Chat window
`#input-bar` | The bottom wrapper, containg the textarea element, send button, and bottom text
`#message-input` | The textarea inside the input bar, used for user input
`#clear-message` | The button used to clear text from the message input
`#send-button ` | The button for submitting the user input
`#status-bar` | The bottom text inside the input bar
`#close-info-button` | The button to close the settings modal
`#language-selector` | The language select container
`#language-picker` | The language select element
`#terms-of-service` | The terms of service link
`#privacy` | The privacy link
`#messages-list` | The messages container
`#topBar` | The top bar container above the message list
`#info-button` | The settings modal button
`.g-message` | The base message selector
`.g-message--is-owned-by-user` | The selector for messages from the end user

**Example:**
```html
<script type="text/javascript">
  window.adaSettings = {
    customStyles: "*{font-size: 14px !important;}#message-input{background-color: white; border: 1px solid #c1c1c1;}",
    ... // The rest of your settings here
  }
</script>
```

#### `greetingHandle` `@type {String}`
This can be used to customize the greeting messages that new users see. This is useful for setting page-specific greetings across your app. The `greetingHandle` should correspond to the title of the Answer you would like to use.

**Example:**
```html
<script type="text/javascript">
  window.adaSettings = {
    greetingHandle: "My Answer",
    ... // The rest of your settings here
  }
</script>
```

#### `language` `@type {String}`
Takes in a language code to programatically set the bot language. Languages must first be turned on in the **Settings > Multilingual** page of your Ada dashboard. Language codes follow the [ISO 639-1 language format](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

**Example:**
```html
<script type="text/javascript">
  window.adaSettings = {
    language: "fr",
    ... // The rest of your settings here
  }
</script>
```

#### `mobileOverlay` `@type {Boolean}`
By default, the Web Chat will open in a new window on mobile devices. If you'd prefer to have it open as an overlay overtop the current window, set this option to `true`.

#### `parentElement` `@type {String|Object}`
Specifies where to mount the `<iframe>` if the default side drawer is not desired. Accepts the `HTMLNode` or `id` of the desired parent element.

**Example:**
```html
<head>
  ...
  <script type="text/javascript">
    window.adaSettings = {
      parentElement: document.getElementById("custom-iframe"),
      ... // The rest of your settings here
    }
  </script>
</head>
<body>
  ...
  <div id="custom-iframe"></div>
  ...
</body>
```

#### `private` `@type {Boolean}`
If set to `true`, this will put Web Chat into "Private" mode. This will cause Web Chat to forget conversation history on refresh. This is effectively the same as setting your Web Chat platform persistence to "Forget After Reload" in the **Settings > Platforms** page of your Ada dashboard. More information on persistence can be found [here](https://ada.support/articles/chatter-persistence/).

---

### Actions
Actions can be called from the global `adaEmbed` object. A list of the available actions is available below:

#### `deleteHistory()`

#### `reset()

#### `setMetaFields(metaFields)` `@param {Object}`
You can use this method to set meta properties for the Chatter. This can be useful for tracking information about your end users, as well as for personalizing their experience. For example, you may wish to track the `email` and `name` for conversation attribution. Once set, this information can be accessed in the email attachment from Handoff Form submissions, or via the Chatter modal in the **Conversations** page of your Ada dashboard. Additionally, the bot can be configured to call the user by name. You can learn more about personalization [here](https://ada.support/articles/personalization/).

#### `start(adaSettings)` `@param {Object}`

#### `stop()`
Tears down your Chaperone instance. You must do this if you wish to create a new Chaperone instance.

#### `toggle()`
Can be used to programatically close the Web Chat view. This method cannot be used with the `parentElement` option.

**Example:**
```javascript
adaBot.setMetaField('email', 'joe-schmoe123@gmail.com');
adaBot.setMetaField('name', 'Joe Schmoe');
```

#### `show()`
Can be used to programatically open the Web Chat view. This is useful if you would like to open the Web Chat automatically when the page loads, or when clicking a custom button.

This method cannot be used with the `parentElement` option.

**Example:**
```html
<button onclick="adaBot.show()">Open Chat</button>
```

#### `tellFrameTo(message)` `@param {String}`
Use this method to manipulate the Web Chat `<iframe>`. Use the table below to see what you can tell the frame to do.

`message` | Description
--- | ---
`focus` | Give window focus to the message input in the `<iframe>`
`blur` | Take window focus away from the message input in the `<iframe>`
`reset` | Resets Chat UI with a new Chatter and history
`deleteHistory` | Clears storage so that a new Chatter will be created upon page refresh

## FAQ
#### Q: How do I set up Ada Chat in mobile?
**A:** Chaperone is only intended to be used in web apps, and is not suitable for native mobile applications. Instead, we recommend you include the URL of your Ada Chat bot [inside a Webview](https://github.com/AdaSupport/docs/blob/nh-chaperone-rewrite/embed-mobile.md). By not using Chaperone you will lose access to the Chaperone options and methods listed above. Fortunately, we have made many of these features available to you via query parameters in your Chat URL.

See the table below for a list of available parameters.

Key | Value | Type | Description
--- | --- | --- | ---
`greeting` | The greeting Answer ID | Query String | Specify a custom greeting
`language` | A supported ISO 639-1 language | Query String | Set the Web Chat language
`*` | Any other key is treated as a meta field | Query String | Used to pass meta informaton about an end user
`private` | `true` or 1 | Query String | Used to forget the Chat session on refresh.

#### Q: How do I customize the look of the Ada Chat button?
**A:** There are many ways to do this, and ultimately this will be up to your team's developers. That being said, we recommend targetting the `button.ada-chat-button` element in your CSS and overriding existing styles.

Please note that we cannot guarantee custom changes will work with future versions of Chaperone.

**Example:**

```
// This line in your CSS
button.ada-chat-button {
  left: 24px; // This will position the Chat button on the left side of the screen
}
```
[**You can experiment with a working example here.**](https://jsfiddle.net/2jh94oru/3/)

#### Q: How do I have the bot only appear during certain hours?
**A:** If the bot should only appear during certain times, you will need to wrap you Ada scripts in a condition to check if the user is within scheduled operation hours. If you only require that certain messages be within a scheduled time window, we recommend that you make use of Scheduled Blocks in the **Answer** page of your Ada dashboard.

#### Q: How do I customize the look and feel of Ada Chat?
**A:** Basic customization, such as client tint colour, can be modified from the **Settings > General** page of your Ada dashboard. If you require additional customization, you can make use of the [customStyles](#customstyles-type-string) Chaperone option above.

## Versioning
Currently, the embed script for Ada Chaperone is versioned. This means that in order to receive new Chaperone updates you will need to upgrade to the latest version. The latest embed script can always be found within this document, or within the Chat modal of the **Settings > Platforms** page in your Ada dashboard.

In the (near) future we intend to release a versionless Chaperone embed script. Stay tuned!

## Questions
Need some help? Get in touch with us at [help@ada.support](mailto:help@ada.support).
