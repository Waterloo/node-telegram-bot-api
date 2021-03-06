[![Build Status](https://travis-ci.org/yagop/node-telegram-bot-api.svg?branch=master)](https://travis-ci.org/yagop/node-telegram-bot-api) [![Coverage Status](https://coveralls.io/repos/yagop/node-telegram-bot-api/badge.svg?branch=master)](https://coveralls.io/r/yagop/node-telegram-bot-api?branch=master)

Node.js module to interact with official [Telegram Bot API](https://core.telegram.org/bots/api). A bot token is needed, to obtain one, talk to [@botfather](telegram.me/BotFather) and create a new bot.

```sh
npm install node-telegram-bot-api
```

```js
var TelegramBot = require('node-telegram-bot-api');

var token = 'YOUR_TELEGRAM_BOT_TOKEN';
// Setup polling way
var bot = new TelegramBot(token, {polling: true});
bot.on('message', function (msg) {
  var chatId = msg.chat.id;
  // photo can be: a file path, a stream or a Telegram file_id
  var photo = 'bot.gif';
  bot.sendPhoto(chatId, photo, {caption: "I'm a bot!"});
});
```

There are some other examples on [examples](https://github.com/yagop/node-telegram-bot-api/tree/master/examples).

* * *

## TelegramBot

Both request method to obtain messages are implemented. To use standard polling, set `polling: true`
on `options`. Notice that [webHook](https://core.telegram.org/bots/api#setwebhook) will need a valid (not self signed) SSL certificate.
Emmits `message` when a message arrives.

See: https://core.telegram.org/bots/api

### Params:

* **String** *token* Bot Token
* **Object** *[options]*
* **Boolean|Object** *[options.polling=false]* Set true to enable polling
* **String|Number** *[options.polling.timeout=4]* Polling time
* **Boolean|Object** *[options.webHook=false]* Set true to enable WebHook
* **String** *[options.webHook.key]* PEM private key to webHook server
* **String** *[options.webHook.cert]* PEM certificate key to webHook server

## getMe()

Returns basic information about the bot in form of a `User` object.

### Return:

* **Promise**

## setWebHook(url)

Specify a url to receive incoming updates via an outgoing webHook.

### Params:

* **String** *url* URL

## getUpdates([timeout], [limit], [offset])

Use this method to receive incoming updates using long polling

See: https://core.telegram.org/bots/api#getupdates

### Params:

* **Number|String** *[timeout]* Timeout in seconds for long polling.
* **Number|String** *[limit]* Limits the number of updates to be retrieved.
* **Number|String** *[offset]* Identifier of the first update to be returned.

### Return:

* **Promise** Updates

## sendMessage(chatId, text, [options])

Send text message.

See: https://core.telegram.org/bots/api#sendmessage

### Params:

* **Number|String** *chatId* Unique identifier for the message recipient
* **Sting** *text* Text of the message to be sent
* **Object** *[options]* Additional Telegram query options

### Return:

* **Promise**

## forwardMessage(chatId, fromChatId, messageId)

Forward messages of any kind.

### Params:

* **Number|String** *chatId* Unique identifier for the message recipient
* **Number|String** *fromChatId* Unique identifier for the chat where the original message was sent
* **Number|String** *messageId* Unique message identifier

### Return:

* **Promise**

## sendPhoto(chatId, photo, [options])

Send photo

See: https://core.telegram.org/bots/api#sendphoto

### Params:

* **Number|String** *chatId* Unique identifier for the message recipient
* **String|stream.Stream** *photo* A file path or a Stream. Can also be a `file_id` previously uploaded
* **Object** *[options]* Additional Telegram query options

### Return:

* **Promise**

## sendAudio(chatId, audio, [options])

Send audio

See: https://core.telegram.org/bots/api#sendaudio

### Params:

* **Number|String** *chatId* Unique identifier for the message recipient
* **String|stream.Stream** *audio* A file path or a Stream. Can also be a `file_id` previously uploaded.
* **Object** *[options]* Additional Telegram query options

### Return:

* **Promise**


## sendChatAction(chatId, action)

Send chat action. Type of `action` to broadcast. `typing` for text messages, `upload_photo` for photos, `record_video` or `upload_video` for videos, `record_audio` or `upload_audio` for audio files, `upload_document` for general files, `find_location` for location data.

See: https://core.telegram.org/bots/api#sendchataction

### Params:

* **Number|String** *chatId* Unique identifier for the message recipient
* **String** *action*  Type of action to broadcast.

### Return:

* **Promise**
