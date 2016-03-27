---
title: Tutorial - Chat Basics
layout: markdown
permalink: /docs/docs/chat-guide/
---

{% raw %}

# OTB Project Documentation

### Tutorial: Chat Basics

##### Commands, Aliases, and Quotes

## Table of Contents

- [Version](#version)
  - [Changelog](#changelog)
- [Notes](#notes)
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
  - [Changing the Count of a Command](#changing-the-count-of-a-command)
  - [Listing Commands](#listing-commands)
  - [Getting the Raw Response of a Command](#getting-the-raw-response-of-a-command)
- [Aliases](#aliases)
  - [Creating an Alias](#creating-an-alias)
  - [Deleting an Alias](#deleting-an-alias)
  - [Listing Aliases](#listing-aliases)
  - [Getting the Command an Alias is Aliased to](#getting-the-command-an-alias-is-aliased-to)
  - [Disabling and Enabling Aliases](#disabling-and-enabling-aliases)
- [Quotes](#quotes)
  - [Adding a Quote](#adding-a-quote)
  - [Removing a Quote](#removing-a-quote)
  - [Getting the ID of a Quote](#getting-the-id-of-a-quote)
  - [Listing Quotes](#listing-quote)
  - [Retrieving a Quote](#retrieving-a-quote)

## Version

Version 1.0

### Changelog

* 1.0
  * Created tutorial

## Notes

For other tutorials, see the [Tutorial Table of Contents](tutorial-toc.html).

If you have any questions or if anything in this tutorial is unclear, please leave a question in the <a href="https://github.com/OTBProject/OTBProject/issues" target="_blank">Issue Tracker</a>, or [contact us](../../contact).

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

Subcommands such as `add` (in `!command add`), and those mentioned later (for commands, aliases, and quotes) are not case sensitive; that is, `!command ADD` is equaly valid. Casing for subcommands in this tutorial is used purely for clarity.

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

You may be wondering at this point how you can make it so that only a moderator can run a command. Or maybe also subscribers? I will discuss how asign a minimum user level to run a command here; you can find more information about user levels and their descriptions [here](reference-user-levels.html).

There are two ways in which you can restrict how a command is run, and both are specified using flags in the `!command add` or `!command set` commands (or in any equivalent commands such as `!setcom`).

What's a flag? A flag is something you add to the command in order to specify more information about how you want the command to be set. Flags start with `--`. For example, you might type `!command set --<flag> <command name> <response>` (don't worry, it will become more clear in a moment). Flags are optional, and if multiple are present, their order does not matter.

#### Minimum User Level for a Command

The flag to assign a minimum user level for a command is `--ul=<user level>` (`ul` for "user level"). For example, suppose you only want moderators (or people with a higher user level) to be able to run your `!example` command. You could add it by typing `!command add --ul=mod !example This is an example command` in chat.

The following is a list of valid markers which can be used with the `--ul=<user level>` flag in place of `<user level>`. If you are confused as to what some of the user levels listed are, see the [tutorial about user levels](reference-user-levels.html).

| User Level | Markers |
|:-----------|:----------|
|[Default](reference-user-levels.html#default)|`default | def | none | any | all`|
|[Subscriber](reference-user-levels.html#subscriber)|`subscriber | sub`|
|[Regular](reference-user-levels.html#regular)|`regular | reg`|
|[Moderator](reference-user-levels.html#moderator)|`moderator | mod`|
|[Super-moderator](reference-user-levels.html#super-moderator)|`super-moderator | super_moderator | smod | sm`|
|[Broadcaster](reference-user-levels.html#broadcaster)|`broadcaster | bc`|

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

### Changing the Count of a Command

The bot stores the number of times each command has been run. While changing the response of the command with `!command set` resets that count to 0, you can also reset it by running the command `!count reset <command name>`.

Another way of resetting the count of a command is:

* `!resetCount <command name>`

For reference, the alias used there is:

* `!resetCount='!count reset'`

If you want to manually set the count of a command (perhaps someone accidentally reset the count), you can do so with the command `!count set <count> <command name>`, where `<count>` is a non-negative integer.

If the count is only slightly off (if you're using a command as a counter and someone accidentally ran the command twice), then you can increase the count by 1 with the command `!count increment <command name>`, or decrease it by 1 with the command `!count decrement <command name>`.

Another way of incrementing the count of a command is:

* `!count inc <command name>`

Another way of decrementing the count of a command is:

* `!count dec <command name>`

### Listing Commands

To list all commands you can run the command `!command list`. (There is a type of command which will not be listed, but you do not need to worry about it. It will be explained elsewhere [missing link]().)

Another way of listing commands is:

* `!commands list`

For reference, the alias used there is:

* `!commands='!command'`

### Getting the Raw Response of a Command

You may want to get the raw response of a command if you discover a typo or decide you want to change the response slightly. What is the raw response? The raw response is the text given as the response when creating the command. "Why don't you just run the command then?", you might ask. There are several special terms you can use when creating a command which get replaced by other text (for example, `[[user]]` will be replaced by the name of the user running the command). Special terms will be described in detail later.

To get the raw response for a command, use the command `!command raw <command name>`.

Another way of getting the raw response for a command is:

* `!commands raw <command name>`

For reference, the alias used there is:

* `!commands='!command'`

## Aliases

The main command for working with aliases is `!alias-meta`. You may say, "That's a really weird and confusing command name. Why would you name it that?" It has that name because easier-to-use aliases are used for most actions, as will become apparent.

### Creating an Alias

To create an alias, use the command `!alias <alias name> <command>`. `<alias name>` must not contain spaces, but `<command>` may. If an alias with the specified name already exists, it is overwritten. For example, to create the already-mentioned `!addcom` alias (which is built-in and does not need to be added manually), you might run the command `!alias !addcom !command add`.

Another way of creating an alias is:

* `!alias-meta set <alias name> <command>`

For reference, the alias used there is:

* `!alias='!alias-meta set'`

If you wish to add an alias only if an alias with the specified name does not exist, you can use the command `!alias-meta add <alias name> <command>` or `!alias-meta new <alias name> <command>`.

### Deleting an Alias

To delete an alias, use the command `!unalias <alias name>`. For example, to remove the `!addcom` alias, you would run the command `!unalias !addcom`.

Other ways of deleting an alias are:

* `!alias-meta delete <alias name>`
* `!alias-meta remove <alias name>`
* `!alias-meta del <alias name>`
* `!alias-meta rm <alias name>`

For reference, the alias used there is:

* `!unalias='!alias-meta delete'`

### Listing Aliases

To list all aliases, use the command `!aliaslist`.

Another way of listing all aliases is:

* `!alias-meta list`

For reference, the alias used there is:

* `!aliaslist='!alias-meta list'`

### Getting the Command an Alias is Aliased to

If you don't remember what command an alias is aliased to, you can run the command `!alias-meta getCommand <alias name>`, and the bot will print the command in chat. (Like commands in general, `getCommand` is not case sensitive.)

For example, if you run the command `!alias-meta getCommand !addcom`, the bot will reply `'!addcom' is aliased to: !command add`.

### Disabling and Enabling Aliases

To disable an alias without deleting it, use the command `!alias-meta disable <alias name>`. The alias will then be ignored if it is used.

To enable an alias again, use the command `!alias-meta enable <alias name>`.

## Quotes

If someone says something funny or memorable on stream or in chat, the bot can store it as a quote, so it can be retrieved and printed later in chat. Quotes can be retrieved either randomly or by an ID number, as will be explained shortly.

The main command for adding and removing quotes is `!quote`; however, `!quotes` is aliased to `!quote` (that is, `!quotes='!quote'`).

### Adding a Quote

To add a quote, use the command `!quote add <quote>`. `<quote>` may contain spaces, and may be as long or short as you wish, as long as a quote with the exact same text does not already exist.

Each new quote is given a numeric ID number (in roughly sequential order).

Other ways of adding a quote are:

* `!quote new <quote>`
* `!quotes add <quote>`
* `!quotes new <quote>`

For reference, the alias used there is:

* `!quotes='!quote'`

### Removing a Quote

To remove a quote, use the command `!quote remove <id>`, where `<id>` is the ID number of the quote. (This will leave a gap in the sequential order of quote IDs, which will be filled when another quote is added.)

If you do not know the ID of a quote, see the following section: [Getting the ID of a Quote](#getting-the-id-of-a-quote).

Other ways of removing a quote are:

* `!quote delete <quote>`
* `!quote del <quote>`
* `!quote rm <quote>`
* `!quotes remove <quote>`
* `!quotes delete <quote>`
* `!quotes del <quote>`
* `!quotes rm <quote>`

For reference, the alias used there is:

* `!quotes='!quote'`

### Getting the ID of a Quote

If you know the full text of a quote, you can use the command `!quote getID <quote>` (where `<quote>` is the full text of the quote) to get the ID of the quote.

Another way of getting the ID of a quote is:

* `!quotes getID <quote>`

For reference, the alias used there is:

* `!quotes='!quote'`

### Listing Quotes

To list the IDs of all quotes, use the command `!quote list`.

Other ways of listing quote IDs are:

* `!quote listIDs`
* `!quote IDs`
* `!quotes list`
* `!quotes listIDs`
* `!quotes IDs`

For reference, the alias used there is:

* `!quotes='!quote'`

### Retrieving a Quote

To have the bot print a random quote, use the command `!getQuote`. To have the bot print a specific quote, use the command `!getquote <id>`, where `<id>` is the ID number of the quote.

There is also a special term which can be used in the text of commands to retrieve a random or specific quote, which is discussed in the [tutorial about building commands]() (not yet written).

{% endraw %}
