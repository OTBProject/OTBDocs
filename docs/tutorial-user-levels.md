---
title: Tutorial - User Levels
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: User Levels

## Table of Contents

- [Version](#version)
- [What are User Levels?](#what-are-user-levels)
- [List of User Levels](#list-of-user-levels)
  - [Internal](#internal)
  - [Broadcaster](#broadcaster)
  - [Super-moderator](#super-moderator)
  - [Moderator](#moderator)
  - [Regular](#regular)
  - [Subscriber](#subscriber)
  - [Default](#default)
  - [Ignored](#ignored)

## Version

1.0

Corresponds to Release 1.0.0+

## What are User Levels?

A user level is a category describing how much power a user has in a channel.

The following is a list of the user levels for OTB in order from greatest to least power.

## List of User Levels

#### Internal

This is a user level used by the bot for certain internal operations. It is a higher user level than even Broadcaster, and any operation which requires this user level can only be performed by the person running/managing the bot.

Type: `Internal/fixed`

#### Broadcaster

This is the user level of the broadcaster/streamer of a channel. It is the highest user level which a chat user can have.

Type: `Determined by livestreaming service`

#### Super-moderator

This is a user level which is meant to be assigned to a select few trusted moderators (such as, for example, users who are editors of your channel on Twitch). A super-moderator has more power than a regular moderator, and modify more bot settings than a regular moderator.

Type: `Assigned through bot`

#### Moderator

This user level corresponds to the moderator status on the streaming service.

Type: `Determined by livestreaming service`

#### Regular

This user level is meant for users who watch streams and participate in chat regularly, and are more trusted than the average person in chat.

Type: `Assigned through bot`

#### Subscriber

This user level corresponds to someone who pays a monthly subscription fee (through the streaming service) to support the streamer.

Type: `Determined by livestreaming service`

#### Default

This user level is the default user level given to anyone who is not in another category.

Type: `Default`

#### Ignored

Users with this user level are unable to run any commands, even commands which Default users can run. It is meant for users who are spamming commands or otherwise using bot commands to be annoying and/or disruptive.

Type: `Assigned through bot`

{% endraw %}
