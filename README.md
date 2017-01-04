# Superslacker

Superslacker is a supervisor "event listener" that sends events from processes that run under [supervisor](http://supervisord.org) to [Slack](https://slack.com). When `superslacker` receives an event, it sends a message notification to a configured `Slack` channel.

`superslacker` uses [Slacker](https://github.com/os/slacker) full-featured Python interface for the Slack API.

## Installation

```
pip install superslacker
```

## Command-Line Syntax

```bash
$ superslacker [-t token] [-c channel] [-n hostname] [-w webhook] [-a attachment] [-r]
```

### Options

```-t TOKEN, --token=TOKEN```

Post a message to Slack using Slack Web API. In order to be able to send messages to Slack, you need to generate your `token` by registering your application. More info can be found [here](https://api.slack.com/web)

```-c CHANNEL, --channel=CHANNEL```

`#channel` to fill with your crash messages.

```-n HOSTNAME, --hostname=HOSTNAME```

Name or identificator of the machine where the events are been generated. This goes in the event message.

```-w WEBHOOK, --webhook=WEBHOOK```

Post a message to Slack using Slack Incoming WebHook. In order to be able to send messages to Slack, you need to configure an `Incoming WebHook` for your Slack account. More info can be found [here](https://api.slack.com/incoming-webhooks)

```-a ATTACHMENT, --attachment=ATTACHMENT```

Add text attachment to message. Attachment will have red color border along the left side.

```-r , --realtime```

Send notifications in a realtime.


## Notes

When using webhook, do not forget properly customize it with proper Icon and Name in Slack.

:ghost: gonna be used as an icon for the message and `superslacker` as a username.


## Configuration
An `[eventlistener:x]` section must be placed in `supervisord.conf` in order for `superslacker` to do its work. See the “Events” chapter in the Supervisor manual for more information about event listeners.

The following example assume that `superslacker` is on your system `PATH`.


```
[eventlistener:superslacker]
command=superslacker --token="slacktoken-slacktoken-slacktoken" --channel="#notifications" --hostname="HOST"
events=PROCESS_STATE,TICK_60
```
