# read_from_chrome_cli

## Extract online articles with Readability and headless Chrome and copies to clipboard

A simple tool that:

1. Attaches to a running Chrome instance
2. Navigates to a given url
3. Injects Readbility.js
4. Waits until a website loads
5. Runs Readability and returns an extracted article
6. Copies the extracted article to clipboard

Headless mode allows much simpler Chrome integration in a server environment and gives Chrome speed and reliability for various web automation tools.

[Headless Chrome](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/) is still under development therefore this guide can change.

This tool uses [Chrome Debugging Protocol](https://developer.chrome.com/devtools/docs/debugger-protocol) to control a Chrome instance.

## For Linux

Install Chrome from a development channel (until headless mode appears in a stable chrome version):

https://www.google.com/chrome/browser/?platform=linux&extra=devchannel

Headless Chrome isn't executed automatically, because it's more reliable to run and manage its process separately.

```
google-chrome-unstable --headless --user-data-dir=/tmp/chrome-new-data --remote-debugging-port=9222

git clone https://github.com/chiraag-kakar/read_from_chrome
```

```js
var chromeReadability = require('./chrome-readability');

var url = 'https://hackernoon.com/13-major-challenges-faced-while-building-a-community-experts-roundup-e3a59aa28fbf';

chromeReadability.extract(url, function(err, article) {
    console.log(article.content);
});
```

## The Javascript Function required to enable copying to clipboard is :

Note :  It will only work for DOM objects

```js
navigator.clipboard.writeText(textData.editor)
```

To make it work for all objects , we can refer [this](https://github.com/electron/electron/blob/master/docs/api/clipboard.md#clipboard) module.


## Limitations:

1. Unlike the normal Chrome mode, the headless mode currently supports only one tab per instance, it means to use this script in parallel more instances on different ports must be executed.













