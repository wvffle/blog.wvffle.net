---
title: Writing Your First Minecraft Bot With JavaScript
created_at: 2020-02-23T18:19:39.600Z
updated_at: 2020-02-23T18:19:39.600Z
image: "./images/unsplash-cPF2nlWcMY4-Daniel-Cheung.jpg"
---

Have you ever wondered if you can create a minecraft bot? Well, you can and it is really simple thanks to the [mineflayer](https://github.com/PrismarineJS/mineflayer) library. This little piece of art maintained by [Romain](https://github.com/rom1504), [me](https://github.com/wvffle) and other contributors is capable of creating advanced bots that can handle commands, bridge chat with discord or even find and dig diamonds.

# Getting started
Obviously first you need to initiate new project or add the dependency to the existing one. Personally I like [yarn](https://yarnpkg.com) much more than npm so I'll go with that.

```shell script
$ yarn init
$ yarn add mineflayer
```

Right now everything is prepared so we can start writing our bot. First we need to include mineflayer and create a bot instance with `mineflayer.createBot()` function.

It takes one parameter of type Object as options and expects some essential values to make our bot work:
- `host` - address of the server you want the bot to connect to
- `port` - port of that server, defaults to `25565`
- `version` - minecraft version that is supported by the server
- `username` - your bot's username
- `password` - your bot's password. This is optional and required only if you login to online-mode servers

```js
import { createBot } from 'mineflayer'

const bot = createBot({
  host: 'localhost',
  port: 25565,
  username: 'wvffle-bot',
  version: '1.12.2'
})
```

Great. Now, when you run `node index.js` and check the player list, you should see that the bot has successfully connected to the server.

> **My bot does not connect! What should I do?!** <br>
> That will be covered later in [this](#the-bot-does-not-connect-and-prints-no-errors) section

# Handling commands, the correct way

```js
const admins = [ 'wvffle' ]

const commands = { 
  exit () {
    bot.exit()
  }   
}

bot.on('whisper', (username, message) => {
  if (!admins.includes(username)) {
    return
  }

  const args = message.split(' ')
  const cmd = args.shift()

  if (cmd in commands) {
    commands[cmd]()
  }
})
```

# I have some troubles! Help me!
## The bot does not connect and prints no errors
There may be many causes of that problem. Three most common of them are:
- Invalid version number
- An unhandled error
- Bot being kicked/banned by the server

<slot name="donate"/>

