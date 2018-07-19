# Embed Ada in Native Mobile App

> Ada can be embedded into a webview inside a native mobile application

## Overview

Ada's chat UI can be embedded into a webpage through [Chaperone](https://github.com/AdaSupport/docs/blob/master/chaperone.md), but what if we wanted to embed the chat UI into a native mobile application? It's easy as pie!

The chat UI is simply a single-page standalone web application that's designed to function equally well on a desktop web browser as on a mobile WebView component.

## Android

Embedding Ada into an Android application is as simple as starting an Activity that presents a [WebView](https://developer.android.com/reference/android/webkit/WebView) view.

To provide a WebView in your own Activity, include a `<WebView>` in your layout, or set the entire Activity window as a WebView during `onCreate()`:

```java
WebView webview = new WebView(this);
setContentView(webview);
```

Then load your bot's Chat UI:

```java
webview.loadUrl("https://<bot-handle>.ada.support/chat/");
```

Lastly, you'll want to enable JavaScript in the webview:

```java
webview.getSettings().setJavaScriptEnabled(true);
```

*Note, you must include the `INTERNET` permissions in your application's Android Manifest File:*

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## iOS
