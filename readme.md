# Botkit and Dialogs

TODO Table of Contents

## Getting Started

TODO

#### dlg()
| Argument | Description
|--- |---
| config | an object containing configuration options

Returns a new Botkit SlackBot controller.

The `config` argument is an object with these properties:

| Name | Type | Description
|--- |--- |---
| debug | Boolean | Enable debug logging
| token | string | dialog bot token
| endpoints | array | list of dialog grpc endpoints

For example:

```javascript
var dlg = require('@dlghq/botkit-module');

var controller = dlg({
    token: process.env.DIALOGS_TOKEN,
    endpoints: [process.env.DIALOGS_ENDPOINT],
    scopes: ['bot'],
});
```

## Event List

In addition to the [core events that Botkit fires](core.md#receiving-messages-and-events), this connector also fires some platform specific events.

In fact, Botkit will receive, normalize and emit any event that it receives from Dialog.

### Incoming Message Events
| Event | Description
|--- |---
| direct_message | the bot received a direct message from a user
| direct_mention | the bot was addressed directly in a channel
| mention | the bot was mentioned by someone in a message
| ambient | the message received had no mention of the bot

### User Activity Events:
| Event | Description
|--- |---
| bot_group_join | the bot has joined a group
| user_group_join | a user has joined a group
| bot_group_left | the bot has left a group
| user_group_left | a user has left a group


## Files

### Receiving

Files sent by other users trigger the `file_share` event.
`message.raw_message.document` contains the file information.

### Sending

#### Regular files

Send a message object with a file property:
```js
bot.reply(message, {
    file: {
        path: '/path/to/file'
    }
})
```

#### Images

Same as regular files, but set `isImage`:

```js
bot.reply(message, {
    file: {
        path: '/path/to/file.jpg',
        image: true
    }
})
```
