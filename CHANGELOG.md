# Changelog

## v1.6.0

### en

#### BREAKING CHANGE

- Telegram bot library has been migrated from `python-telegram-bot` (which uses HTTP Bot API and is synchronous)
  to `telethon` (which uses MTProto Bot API and is asynchronous)
    - However, to use MTProto Bot API, an API key is needed. The bot has 7 built-in API keys (collected from the
      Internet) and in most cases it should not be unable to log in. But if so, please obtain your own API key (
      see [docker-compose.yml.sample](https://github.com/Rongronggg9/RSS-to-Telegram-Bot/blob/53f11a473933e620d707c9d15f6d48737bd7a982/docker-compose.yml.sample#L43)
      for details)

#### New features

- Thanks to the migration of Telegram bot library, bot can now connect to its DC directly, need not detour through the
  HTTP Bot API and keep polling to get new messages. Which makes the bot receive and reply messages more rapidly and
  lightweightedly. Even if the HTTP Bot API is down, the bot can still run unaffectedly. (more
  details: [Advantages of MTProto over Bot API](https://docs.telethon.dev/en/latest/concepts/botapi-vs-mtproto.html#advantages-of-mtproto-over-bot-api)
  , [MTProto vs HTTP Bot API](https://github.com/LonamiWebs/Telethon/wiki/MTProto-vs-HTTP-Bot-API))
- Support parsing more HTML elements
    - `<iframe>`
    - `<video><source><source>...</video>`
    - `<code>`
    - `<pre>`
- Support OPML importing and exporting
- Support sending too-long post via Telegraph (env var `TELEGRAPH_TOKEN` must be set)
- Support redis as db
    - Note: This is a workaround for deploying the bot on [railway.app](), will be dropped in the future
- Support arm64 (docker build)
- Support resending a message using a media relay server if Telegram cannot send a message with media due to Telegram
  server instability or network instability between media server and Telegram server
- Support colored logging
- `docker-compose.yml.sample`
- `/version` command to check bot version
- Automatically use proxy if global proxy (env var `SOCKS_PROXY`/`HTTP_PROXY`) set

#### Changes

- Assign feed monitoring tasks to every minute, instead of executing all at once each `DELAY`
    - Thus, env var `DELAY` can only be 60~3600
    - Note: env var `DELAY` will be deprecated in the future
- Recognize a post by its `guid`/`id` instead of `link`
- Simplify the output of `/list`
- Bump Python to 3.9 (docker build)
- Minor fixes

### zh-Hans

#### ????????????

- ??? Telegram ????????????????????? HTTP Bot API ???????????? `python-telegram-bot` ???????????? MTProto Bot API ???????????? `telethon`
    - ???????????? API key ????????????????????????????????? 7 ???????????? API key?????????????????????????????????????????????????????????????????????????????? API key (
      ?????? [docker-compose.yml.sample](https://github.com/Rongronggg9/RSS-to-Telegram-Bot/blob/53f11a473933e620d707c9d15f6d48737bd7a982/docker-compose.yml.sample#L43)
      ????????????)

#### ?????????

- ?????? Telegram bot ???????????????bot ????????????????????? bot ????????? DC??????????????? HTTP Bot API?????????????????????????????????????????????????????????????????????????????????????????????????????????????????? ?????? HTTP Bot API
  ?????????bot ????????????????????? (
  ?????? [Advantages of MTProto over Bot API](https://docs.telethon.dev/en/latest/concepts/botapi-vs-mtproto.html#advantages-of-mtproto-over-bot-api)
  ??? [MTProto vs HTTP Bot API](https://github.com/LonamiWebs/Telethon/wiki/MTProto-vs-HTTP-Bot-API))
- ???????????????????????????
    - `<iframe>`
    - `<video><source><source>...</video>`
    - `<code>`
    - `<pre>`
- ?????? OPML ????????????
- ???????????????????????? Telegraph ?????? (??????????????? `TELEGRAPH_TOKEN` ????????????)
- ???????????? redis ???????????????
    - ???????????????????????? [railway.app]() ???????????????????????????????????????????????????????????????
- ?????? arm64 (docker ??????)
- ??????????????? Telegram ????????????????????? Telegram ?????????????????????????????????????????????????????????????????? Telegram ?????????????????????????????????????????????????????????????????????????????????
- ??????????????????
- `docker-compose.yml.sample`
- ???????????? bot ????????? `/version` ??????
- ??????????????????????????? (???????????? `SOCKS_PROXY`/`HTTP_PROXY`)??????????????????

#### ??????

- ??? feed ???????????????????????????????????????????????? `DELAY` ?????????????????????
    - ????????????????????? `DELAY` ????????????????????? 60~3600
    - ????????????????????? `DELAY` ??????????????????
- ?????? `guid`/`id` ??????????????? post???????????? `link`
- ????????? `/list` ?????????
- ????????? Python 3.9 (docker ??????)
- ???????????????

## v1.5.0

### en

- Post parser is completely rewritten, more stable and can keep text formatting as much as possible
- GIF Support
- When the message is more than 10 pieces of media, send it in pieces
- Support video and pictures to be mixed in the same message arbitrarily
- Invalid media are no longer directly discarded, but attached to the end of the message as a link
- Automatically determine whether the title of the RSS feed is auto-filled, if so, omit the title
- Automatically show the author name
- Automatically replace emoji shortcodes with emoji
- Automatically replace emoji images with emoji or its description text
- When an image cannot be sent due to the instability of telegram api, the image server will be automatically replaced
  and resent
    - Only for Weibo images, non-Weibo images will be attached to the end of the message as a link
- Improve the text length counting method, no longer cause the message to be divided wrongly due to a long link URL
- Change the user-agent, because some websites have banned the UA of Requests
- Logging improvement

### zh-Hans

- **????????????????????????????????????????????????????????????????????????**
    - **???????????????????????? RSS ??????????????????**
    - **??????????????? RSS ???????????????????????????**
- **?????? GIF**
- **???????????? 10 ??????????????????????????????**
- **???????????????????????????????????????????????????**
- ????????????????????????????????????????????????????????????????????????
- ???????????? RSS ?????????????????????????????????????????????????????????????????????
- ?????????????????????
- ???????????? emoji shortcodes ??? emoji
- ???????????????????????????????????????????????? emoji ??????????????????
- ??? telegram api ?????????????????????????????????????????????????????????????????????
    - ??????????????????????????????????????????????????????????????????????????????????????????
- ??????????????????????????????????????????????????? url ????????????????????????????????????
- ?????? user-agent??????????????????????????? requests UA ?????????
- ?????????????????????

## v1.0.0

initial public release