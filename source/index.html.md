---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Introduction

Welcome to the Boba Gang API! You can use our API to access endpoints, which can keep track of your website errors, performance, and users characteristics!

This documentation page is powered by [Slate](https://github.com/lord/slate)

# Authentication

To access our analytics, you need to login to our website.

If you do not want to create a new account, you can login through this username and password:

Username | Password
--------- | -----------
kevin | go

Or you can also create an account by filling in a form in [sign up](http://134.209.48.230/login)

# Collector

## Post error

```javascript
window.onerror = function (msg, url, lineNo, columnNo, error) {
  //session id
  var session = document.cookie;
  //user-agent
  var userAgent = navigator.userAgent;

  //timestamp
  var d = new Date();
  var time = d.getTime();
  var jsonError = {
    "message": msg,
    "url": url,
    "lineno": lineNo,
    "colno": columnNo,
    "error": String(error),
    "session_id": session,
    "user_agent": userAgent,
    "time_stamp": time
  };

  console.log(JSON.stringify(jsonError));

  var url = "http://134.209.48.230/client/errorcollector";
  var params = JSON.stringify(jsonError);
  var xhr = new XMLHttpRequest();
  xhr.open("POST", url, true);

  //Send the proper header information along with the request
  xhr.setRequestHeader("Content-type", "application/json");
  xhr.send(params);

  return false;
}
```
> The above command will update the database JSON structured like this:

```json
[
  {
    "id": 1,
    "session_id": "s%3AUgusC0yc0v3e5dzyBz3HXQ-YFGhPcXrV.In1MFoeT8rijs8cOdscQHx2M5cJDNLD9jSFWMxxJChI",
    "time_stamp": 1551568450288,
    "url":"http: //134.209.48.230/vun",
    "lineno": 11,
    "colno": 65,
    "message": "Uncaught ReferenceError: asdf is not defined",
    "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36"
  }
]
```

This endpoint updates the database error log.

### HTTP Request

`POST http://134.209.48.230/client/errorcollector`


### Query Parameters

Parameter | Description
--------- | -----------
message | If set to true, the result will also include cats.
url | The url of the error events triggered
lineno | The line number of your code triggering the error
colno | The column number of your code triggering the error
error | The error object of the error in a website
session_id | The session id of a user triggering the error
user_agent | The user agent of a user triggering the error
time_stamp | The timestamp of the error

<aside class="success">
Remember — a boba gang is only for boba lovers!
</aside>

## Post a new user characteristic

```javascript
var screenHeight = window.screen.availHeight;
var screenWidth = window.screen.availWidth;
var weblink = window.location.href;
var jsonClient = {
  "screenHeight": screenHeight,
  "screenWidth": screenWidth,
  "url": weblink
};

var url = "http://134.209.48.230/client/clientcollector";
var params = JSON.stringify(jsonClient);
var xhr = new XMLHttpRequest();
xhr.open("POST", url, true);
//Send the proper header information along with the request
xhr.setRequestHeader("Content-type", "application/json");
xhr.send(params);
```

> The above command will update the database JSON structured like this:

```json
{
  "id": 2,
  "session_id": "s%3AUgusC0yc0v3e5dzyBz3HXQ-YFGhPcXrV.In1MFoeT8rijs8cOdscQHx2M5cJDNLD9jSFWMxxJChI",
  "os": "iOS",
  "mobile": "Iphone",
  "browser": "Chrome",
  "screenHeight": 812,
  "screenWidth": 375,
  "url": "http://134.209.48.230/vun"
}
```

This endpoint updates the database client characteristic log.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### HTTP Request

`POST http://134.209.48.230/client/clientcollector`

### URL Parameters

Parameter | Description
--------- | -----------
screenHeight | The screen height resolution of the device
screenWidth | The screen width resolution of the device
url | The url of that the client entered in your website

<aside class="success">
Remember — a boba gang is only for boba lovers!
</aside>


## Post a user's performance

```javascript
window.onload = function() {
  //connection of the user
  var connection = navigator.connection.effectiveType;
  var timeOrigin = window.performance.timeOrigin;
  var connectStart = window.performance.timing.connectStart;
  var connectEnd = window.performance.timing.connectEnd;
  var domComplete = window.performance.timing.domComplete;
  var domContentLoadedEventEnd = window.performance.timing.domContentLoadedEventEnd;
  var domContentLoadedEventStart = window.performance.timing.domContentLoadedEventStart;
  var domInteractive = window.performance.timing.domInteractive;
  var requestStart = window.performance.timing.requestStart;
  var responseStart = window.performance.timing.responseStart;
  var responseEnd = window.performance.timing.responseEnd;
  var weblink = window.location.href;
  var byte_per_sec = navigator.connection.downlink;

  var jsonSpeed = {
    "connection": connection,
    "timeOrigin": timeOrigin,
    "connectStart": connectStart,
    "connectEnd": connectEnd,
    "domComplete": domComplete,
    "domContentLoadedEventEnd": domContentLoadedEventEnd,
    "domInteractive": domInteractive,
    "requestStart": requestStart,
    "responseStart": responseStart,
    "responseEnd": responseEnd,
    "byte_per_sec": byte_per_sec,
    "url": weblink
  };

  var url = "http://134.209.48.230/client/speedcollector";
  var params = JSON.stringify(jsonSpeed);
  var xhr = new XMLHttpRequest();
  xhr.open("POST", url, true);
  //Send the proper header information along with the request
  xhr.setRequestHeader("Content-type", "application/json");
  xhr.send(params);
};
```

> The above command will update the database JSON structured like this:

```json
{
  "id": 1,
  "session_id" : "s%3AUgusC0yc0v3e5dzyBz3HXQ-YFGhPcXrV.In1MFoeT8rijs8cOdscQHx2M5cJDNLD9jSFWMxxJChI",
  "connection": "4g",
  "timeOrigin": "1551485636915.87",
  "connectStart": "1551485636951",
  "connectEnd": "1551485636979",
  "domComplete": "1551485637157",
  "domContentLoadedEventEnd": "1551485637110",
  "domInteractive": "1551485637109",
  "requestStart": "1551485637032",
  "responseStart": "1551485637033",
  "responseEnd": "1551485637034",
  "url": "http://134.209.48.230/vun",

}
```

This endpoint updates the database performance logs.

### HTTP Request

`POST http://134.209.48.230/client/speedcollector`

### URL Parameters

Parameter | Description
--------- | -----------
connection | The connection of the user entering the website (e.g. 4g,3g, etc)
timeOrigin | The timestamp of the start time of the performance measurement
connectStart | The timestamp the web starts connection
connectEnd | The timestamp the web ends connection
domComplete | The timestamp the dom is parsed
domContentLoadedEventEnd | The timestamp the dom tree content is parsed
domContentLoadedEventStart | The timestamp the dom tree content is being parsed
domInteractive | The timestamp the dom tree becomes interactive
requestStart | The timestamp the request is being processed
responseStart | The timestamp the response is being processed
responseEnd | The timestamp the response is processed
byte_per_sec | The performance in bytes per seconds downloaded by a user
url | The url of that the client entered in your website

<aside class="success">
Remember — a boba gang is only for boba lovers!
</aside>