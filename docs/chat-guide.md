---
title: Chat Documentation
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: How to Make the Bot Do Things

## Table of Contents

- [Version](#version)
  - [Changelog](#changelog)
- [Background](#background)
  - [What are Commands?](#what-are-commands)
  - [What are Aliases?](#what-are-aliases)
- [Commands](#commands)
  - [Custom Commands](#custom-commands)
    - [Adding a Command](#adding-a-command)
    - [Setting a Command](#setting-a-command)
  - [Restrictions on Commands (and How to Use Flags)](#restrictions-on-commands-and-how-to-use-flags)
    - [Minimum User Level for a Command](#minimum-user-level-for-a-command)
    - [Minimum Number of Arguments for a Command](#minimum-number-of-arguments-for-a-command)
  - [Deleting a Command](#deleting-a-command)
  - [Disabling and Enabling Commands](#disabling-and-enabling-commands)
  - [Renaming Commands](#renaming-commands)
  - [Changing the Minimum User Level](#changing-the-minimum-user-level)
  - [Changing the Minimum Number of Arguments](#changing-the-minimum-number-of-arguments)
  - [Resetting the Count of a Command](#resetting-the-count-of-a-command)

## Version

Version 1.0 [WIP]

### Changelog
* 1.0

## Background

There are a few terms which will be useful to understand before discussing how to use them in chat.

### What are Commands?

A command is a word which the bot will respond to if it is the first word in a message. Commands often start with an exclamation mark, such as `!example`, but they can be any string of characters without a space in them. Commands are not case sensitive, so `!ExaMPle` is equivalent to `!example`.

### What are Aliases?

An alias is a word which represents another word or group of words. Like commands, aliases are only processed by the bot if they are the first word of a message. However, an alias can expand into a command and parameters (other text after the command) for the command, to make running certain commands easier. If an alias expands to something which is not a command or another alias, it won't do anything. Like commands, aliases are not case sensitive.

For example, `!addcom` is said to be "aliased" to `!command add` because if you type `!addcom !example example response`, `!addcom` will be replaced (during processing) by `!command add`, making it as if you had typed `!command add !example example response`. An alias will sometimes be denoted as `<alias>='<expansion>'`. In this example, `!addcom='!command add'`.

A given alias will not be processed more than once per message. What does that mean? Suppose you have two aliases, `!alias-1='!alias-2 and then some text'` and `!alias-2='!alias-1'`. If someone types `!alias-1` in chat and the bot processes it, it will replace `!alias-1` with `!alias-2 and then some text`, and then in turn replace that with `!alias-1 and then some text`. However, it will stop there, and will not replace `!alias-1` with its corresponding text again in that message. If `!alias-1` is also a command, it will be run; otherwise, nothing will happen.

The built-in commands for OTBProject tend to have a lot of aliases in order to be easily usable by people already familiar with the commands from other bots, and to avoid certain confusions of other bots.

## Commands

The main command for creating, deleting, modifying, and listing commands is `!command`. To avoid some confusions I've experienced with other bots, `!commands` is aliased to `!command`; that is to say, anywhere where a command is given as `!command <something>`, you can instead type `!commands <something>`.

### Custom Commands

There are two ways to add a command: you can add the new command only if it doesn't already exists, or you can overwrite the command if it already exists, and add it if it does not. For purposes of this guide, I will refer to the former as "adding a command", and the latter as "setting a command".

#### Adding a Command

The basic way of adding a command is `!command add <command name> <response>`. For example, suppose you want to add a command `!example`, for which the response is `This is an example command`. You would type `!command add !example This is an example command` in chat, and the bot would add the new command `!example`. As mentioned previously, `<command name>` cannot contain any spaces.

Other ways of adding a command (some of which you may be familiar with from other bots) are:
* `!command new <command name> <response>`
* `!addcom <command name> <response>`
* `!commands add <command name> <response>`
* `!commands new <command name> <response>`

For reference, the aliases used there are:
* `!addcom='!command add'`
* `!commands='!command'`

#### Setting a Command

Similar to adding a command, you would type `!command set <command name> <response>` to set a command. If there was already a command with the specified name, it gets overwritten.

Other ways of setting a command are:
* `!command edit <command name> <response>`
* `!setcom <command name> <response>`
* `!editcom <command name> <response>`
* `!commands set <command name> <response>`
* `!commands edit <command name> <response>`

For reference, the aliases used there are:
* `!setcom='!command set'`
* `!editcom='!command set'`
* `!commands='!command'`

### Restrictions on Commands (and How to Use Flags)

You may be wondering at this point how you can make it so that only a moderator can run a command. Or maybe also subscribers? I will discuss how asign a minimum user level to run a command here, though descriptions of all of the user levels will come a bit later.

There are two ways in which you can restrict how a command is run, and both are specified using flags in the `!command add` or `!command set` commands (or in any equivalent commands such as `!setcom`).

What's a flag? A flag is something you add to the command in order to specify more information about how you want the command to be set. Flags start with `--`. For example, you might type `!command set --<flag> <command name> <response>` (don't worry, it will become more clear in a moment). Flags are optional, and if multiple are present, their order does not matter.

#### Minimum User Level for a Command

The flag to assign a minimum user level for a command is `--ul=<user level>` (`ul` for "user level"). For example, suppose you only want moderators (or people with a higher user level) to be able to run your `!example` command. You could add it by typing `!command add --ul=mod !example This is an example command` in chat.

The following is a list of valid markers which can be used with the `--ul=<user level>` flag in place of `<user level>`. If you are confused as to what some of the user levels listed are, don't worry; they will be explained later.

| User Level | Markers |
|:-----------|:----------|
|Default|`default | def | none | any | all`|
|Subscriber|`subscriber | sub`|
|Regular|`regular | reg`|
|Moderator|`moderator | mod`|
|Super Moderator|`super-moderator | super_moderator | smod | sm`|
|Broadcaster|`broadcaster | bc`|

#### Minimum Number of Arguments for a Command

What are arguments? Arguments (sometimes referred to as parameters) are words following the command. For example, if you run a command `!example these are some arguments`, then you ran the command with four arguments: `these`, `are`, `some`, and `arguments`.

Why would you want to have a minimum number of arguments for a command though? Well suppose you have a command which creates a multi-stream link. It wouldn't really make any sense to run the command without specifying some other stream to put in the multi-stream link, so you might want to require at least one argument to specify someone you're streaming with.

So how would you specify a minimum number of arguments? With the flag `--ma=<number>` (`ma` for "minimum arguments"). `<number>` must be a non-negative whole number (0 or higher). If you wanted to require the `!example` command to be run with at least two arguments in order to respond, you would could add it with the command `!command add --ma=2 !example This is an example command`.

If you wanted `!example` to have a minimum user level of moderator and require at least 2 arguments, you could create it with `!command add --ul=mod --ma=2 !example This is an example command` or `!command add --ma=2 --ul=mod !example This is an example command` (or use any variant of `!command add`, such as `!addcom`).

### Deleting a Command

A command can be removed by typing `!command delete <command name>`.

Other ways of deleting a command are:
* `!command remove <command name>`
* `!command del <command name>`
* `!command rm <command name>`
* `!delcom <command name>`
* `!commands delete <command name>`
* `!commands remove <command name>`
* `!commands del <command name>`
* `!commands rm <command name>`

For reference, the aliases used there are:
* `!delcom='!command delete'`
* `!commands='!command'`

### Disabling and Enabling Commands

You can prevent the bot from responding to a command without deleting it by instead disabling it. A command can easily be disabled by running the command `!command disable <command name>`. For example, to disable the `!example` command, you would type `!command disable !example` in chat.

Other ways of disabling a command are:
* `!disable <command name>`
* `!commands disable <command name>`

For reference, the aliases used there are:
* `!disable='!command disable'`
* `!commands='!command'`

You can enable a command again with the command `!command enable <command name>`.

Other ways of enabling a command are:
* `!enable <command name>`
* `!commands enable <command name>`

For reference, the aliases used there are:
* `!enable='!command enable'`
* `!commands='!command'`

### Renaming Commands

To rename a command, you don't need to delete it and re-add it with a new name. You can just use the command `!rename <old command name> <new command name>` (as long as a command with the new name does not already exist).

For example, suppose you want to rename the previously mentioned command `!example` to `!overused-example`. You would type `!rename !example !overused-example` in chat, and the bot would then respond to `!overused-example` and not `!example`.

### Changing the Minimum User Level

To change the user level required to run an existing command, you can use the command `!setExecUL <command name> <user level>`, where `<user level>` is one of the user level markers from [the table earlier](#minimum-user-level-for-a-command).

(As mentioned earlier, commands are not case sensitive, so `!setexecul` works just as well. The casing used here is just to help make the meaning of the command clearer.)

### Changing the Minimum Number of Arguments

To change the minimum number of arguments for an existing command, you can use the command `!setMinArgs <command name> <min args>`, where `<min args>` is a whole number greater than or equal to 0, [as described earlier](#minimum-number-of-arguments-for-a-command).

### Resetting the Count of a Command

The bot stores the number of times each command has been run. While changing the response of the command with `!command set` resets that count to 0, you can also reset it by running the command `!resetCount <command name>`.

## Aliases

{% endraw %}
