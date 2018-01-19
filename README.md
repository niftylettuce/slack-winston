# slack-winston

[![NPM version][npm-image]][npm-url]
[![NPM downloads][npm-downloads]][npm-url]
[![MIT License][license-image]][license-url]

> A [Slack][slack] transport for [winston][winston].

> **NOTE**: This package was created because `winston-slack` did not have similar code
structure to `winston-hipchat` (switched from using HipChat &rarr; Slack and wanted consistency).

**API change notice:** 1.x has made potentially breaking changes to the modules options. The `token` field is no longer required as the slack API no longer uses it. The username and emoji field now function differently. See the [usage](#usage) section for more details.

## Index

* [Install](#install)
* [Usage](#usage)
* [Credits](#credits)
* [License](#license)


## Install

```bash
npm install -S winston slack-winston
```


## Usage

```js
var winston = require('winston')
var slackWinston = require('slack-winston').Slack

var options = {
  domain: 'my-domain',
  token: 'my-slack-incoming-webhook-token',
  webhook_url: 'my-slack-incoming-webhook-url',
  channel: 'general',
  level: 'warn'
}

winston.add(slackWinston, options)
```

Many options can be seen in the [Slack API docs](https://api.slack.com/methods/chat.postMessage).

* __level:__ Level of messages that this transport should log
* __silent:__ If true, will not log messages
* __webhook_url:__ Required. Slack incoming webhook url, _if your webhook integration is old for some reason then you may prefer to use the domain and token approach instead_.
* __domain:__ Required if webhook_url is not provided. Domain of Slack (e.g. "foo" if "foo.slack.com")
* __token:__ Required if webhook_url is not provided. The token provided by slack
* __channel:__ Required. Channel of chat (e.g. "#foo" or "@foo")
* __username:__ Username of the incoming webhook Slack bot, if this is not set then slack will use the integration (webhook) configuration settings.
* __icon_emoji:__ Icon of bot, if this is not set then slack will use the integration (webhook) configuration settings.
* __message:__ [lodash templates](http://lodash.com/docs#template). Gets passed the `{{message}}`, `{{level}}`, and `{{meta}}` as a JSON string. If not specified, it will print a default of `{{message}}\n\n{{meta}}`.  **Note that this gets sent as the `text` field in the payload per Slack requirements.**
* __queueDelay:__ Delay time (ms) between messages in queue (defaults to 500)

## Credits

* Based on [winston-hipchat](https://github.com/joeybaker/winston-hipchat) by [Joey Baker](https://github.com/joeybaker)
* Based on [winston-loggly](https://github.com/indexzero/winston-loggly) by [Charlie Robbins](http://blog.nodejitsu.com)


## License

[MIT][license-url]


[license-image]: http://img.shields.io/badge/license-MIT-blue.svg?style=flat
[license-url]: LICENSE
[slack]: http://slack.com
[winston]: https://github.com/flatiron/winston
[npm-image]: http://img.shields.io/npm/v/slack-winston.svg?style=flat
[npm-url]: https://npmjs.org/package/slack-winston
[npm-downloads]: http://img.shields.io/npm/dm/slack-winston.svg?style=flat
