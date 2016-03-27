---
title: Tutorial - Building Commands
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: Building Commands

## Table of Contents

- [Version](#version)
- [Overview](#overview)
- [Structure of Terms](#structure-of-terms)
- [Modifiers](#modifiers)
- [Embedded Strings](#embedded-strings)
- [Terms](#terms)
- [Other Notes](#other-notes)
- [Advanced Examples](#advanced-examples)

## Version

1.0

## Overview

This tutorial is about how to make commands which are more than a simple, unchanging sentence. It will describe how to build commands which include the name of the person running the command, an argument provided to the command, and much more.

Special terms are used to specify a value which may be different each time a command is run. Each term is replaced by string when the command is run. (A string is a combination of letters, numbers or symbols, often a word or sentence.)

## Structure of Terms

The general structure of any term is:

```
[[term.modifier{{embedded string}}]]
```

but it may be as simple as:

```
[[term]]
```

That may seems somewhat confusing and unclear, but will hopefully be less so after we break it down.

* All terms are enclosed by `[[` and `]]`. If either of these are used in a command not in the context of a term, other terms in the command's response will not be processed properly or at all.
* All terms may optionally be followed by a `.` and a [modifier](#modifiers).
* All terms may optionally be followed by one or more [embedded strings](#embedded-strings). Embedded strings follow the modifier if it is present, or the term if there is no modifier. Each embedded string is enclosed by `{{` and `}}`.
* With the exception of embedded strings, no spaces are allowed in a term (inside of `[[` and `]]`).

## Modifiers

A modifier allows you to customize the capitalization of the string returned by a term.
For example, if there was a term `[[example]]` which got replaced by the string `this is an EXAMPLE`, then `[[example.upper]]` would get replaced by `THIS IS AN EXAMPLE`. (Please note that `[[example]]` is not actually a term.)

The valid modifiers and their descriptions are listed in the table below. They are case sensitive. If an invalid modifier (one not specified below) is given, it is ignored. The previously mentioned `[[example]]` term is used as an example for each modifier.

| Modifier | Description | Example |
|:---------|:------------|:--------|
|`lower`|The string is made entirely lowercase.|`this is an example`|
|`upper`|The string is made entirely uppercase.|`THIS IS AN EXAMPLE`|
|`first_cap`|The first letter of the string is made uppercase. All other letters are made lowercase.|`This is an example`|
|`word_cap`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are made lowercase.<br>Identical to `first_cap` for anything which is a single word.|`This Is An Example`|
|`first_cap_soft`|The first letter of the string is made uppercase. All other letters are not changed.|`This is an EXAMPLE`|
|`word_cap_soft`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are not changed.<br>Identical to `first_cap_soft` for anything which is a single word.|`This Is An EXAMPLE`|

Modifiers can be used for any term. There are certain terms for which modifiers have no effect, but even in those cases they do no harm.

## Embedded Strings

An embedded string is a string enclosed in `{{` and `}}` which provides extra information to a term. For example, it might provide a default value for the term if some other value is missing. Embedded strings are necessary, especially for more advanced terms, to allow greater functionality.

Unlike the rest of the term, an embedded string may contain spaces, and may even contain other terms. They may also be empty (`{{}}`) if you so desire.

If a term expects more embedded strings than you've given it, it will treat any missing embedded strings as empty. For example, if you use the term `[[example{{string 1}}{string 2}}]]`, but the term `[[example]]` uses three embedded strings, it will treat the third embedded string as empty; that is, it will be as if you had used the term as `[[example{{string 1}}{{string 2}}{{}}]]`.

## Terms

| Term | Description |
|:-----|:------------|
|`[[user]]`|Returns the name of the user who ran the command.<br><br>`[NthPortal] !command set !example Hello [[user]]! How are you today?`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Hello nthportal! How are you today?`|
|`[[bot]]`|Returns the bot's username.<br><br>`[NthPortal] !command set !example My name is: [[bot]]`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] My name is: otb`|
|`[[channel]]`|Returns the channel in which the command was run.<br><br>`[NthPortal] !command set !example This is [[channel]]'s channel`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] This is maddiiemaneater's channel`|
|`[[service]]`|Returns the name of the service the bot is connected to ("Twitch" or "Beam").<br><br>`[NthPortal] !command set !example I am connected to [[service]]`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] I am connected to Beam`|
|`[[count]]`|Returns the number of times the command has been run since it was created or since it was last modified.<br><br>`[NthPortal] !command set !example This command has been run [[count]] time(s)`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] This command has been run 1 time(s)`<br><br>`[NthPortal] !example`<br>`[OTB] This command has been run 2 time(s)`|
|`[[numargs]]`|Returns the number of arguments with which the command was run.<br><br>`[NthPortal] !command set !example This command was run with [[numargs]] arguments`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] This command was run with 0 arguments`<br><br>`[NthPortal] !example one two three`<br>`[OTB] This command was run with 3 arguments`|
|`[[args{{default}}]]`|Returns all arguments with which the command was run (separated by spaces). If the command was run without arguments, it returns the first embedded string.<br><br>`[NthPortal] !command set !example Welcome to the stream [[args{{someone}}]]!`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Welcome to the stream someone!`<br><br>`[NthPortal] !example Fred and George`<br>`[OTB] Welcome to the stream Fred and George!`|
|`[[argN{{default}}]]`|Returns the `N`th argument, where `N` is a whole number greater than 0. If the command is run with fewer than `N` arguments, it returns the first embedded string.<br><br>`[NthPortal] !command set !example That is a [[arg1{{lamp}}]] and a [[arg2{{hat}}]]!`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] That is a lamp and a hat!`<br><br>`[NthPortal] !example table`<br>`[OTB] That is a table and a hat!`<br><br>`[NthPortal] !example table chair`<br>`[OTB] That is a table and a chair!`|
|`[[fromargN{{default}}]]`|Returns all the arguments from the `N`th argument and on (separated by spaces). `N` is a whole number greater than 0. If the command is run with fewer than `N` arguments, it returns the first embedded string.<br><br>`[NthPortal] !command set !example When [[arg1]] joins the stream, shout [[fromarg2{{something}}]]!`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example Maddiie`<br>`[OTB] When Maddiie joins the stream, shout something!`<br><br>`[NthPortal] !example Maddiie Happy Birthday`<br>`[OTB] When Maddiie joins the stream, shout Happy Birthday!`|
|`[[quote]]` or `[[quote{{ID}}]]`|Returns a random quote from the quote database if the first embedded string is empty or missing. If the first embedded string is not empty, it uses that embedded string as an ID, and returns the quote with the specified ID (if it exists, or an empty string if it does not exist or the ID is invalid).<br><br>`[NthPortal] !command set !example Quote: [[quote{{[[arg1]]}}]]`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Quote: Example quote with ID 9`<br><br>`[NthPortal] !example`<br>`[OTB] Quote: Example quote with ID 2`<br><br>`[NthPortal] !example 4`<br>`[OTB] Quote: Example quote with ID 4`|
|`[[countof{{command}}]]`|Returns the count of the command specified as the first embedded string.<br><br>`[NthPortal] !command set !example Count of '!command': [[countof{{!command}}]]`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Count of '!command': 1`|
|`[[ifargs{{some args}}{{no args}}]]`|Returns the first embedded string if at least one argument was given, or the second embedded string if no arguments were given.<br><br>`[NthPortal] !command set !example Were there any args? [[ifargs{{Yes}}{{Nope, sorry}}]].`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Were there any args? Nope, sorry.`<br><br>`[NthPortal] !example hat`<br>`[OTB] Were there any args? Yes.`|
|`[[ifargN{{N args}}{{fewer than N args}}]]`|Returns the first embedded string if at least `N` arguments were given, or the second embedded string if fewer than `N` arguments were given. `N` is a whole number greater than 0.<br><br>`[NthPortal] !command set !example Were there 3 args? [[ifarg3{{Yes}}{{Nope, sorry}}]].`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example one two`<br>`[OTB] Were there 3 args? Nope, sorry.`<br><br>`[NthPortal] !example one two three`<br>`[OTB] Were there 3 args? Yes.`|
|`[[foreach{{prepend}}{{append}}]]`|For each argument provided, returns the first embedded string, the argument, and then the second embedded string. If a modifier is used, it is applied to each argument (but not to the embedded strings). Spaces are not added between arguments.<br><br>`[NthPortal] !command set !example Tags: [[foreach{{<}}{{>}}]].`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example one two three`<br>`[OTB] Tags: <one><two><three>`|
|`[[equal{{string 1}}{{string 2}}{{if same}}{{if different}}]]`|If the first two embedded strings are the same, then it returns the third embedded string. If not, it returns the fourth embedded string.<br><br>`[NthPortal] !command set !example Hello? [[equal{{[[user]]}}{{maddiiemaneater}}{{Ohai Maddiie!}}{{You're not Maddiie D:}}]].`<br>`[OTB] Set command '!example'.`<br><br>`[NthPortal] !example`<br>`[OTB] Hello? You're not Maddiie D:`<br><br>`[MaddiieManeater] !example`<br>`[OTB] Hello? Ohai Maddiie!`|

## Other Notes

Some of the terms listed above may sometimes produce an empty response. For example, if `[[args]]` is used without a default value, and the command is not run with any arguments, then `[[args]]` will be replaced by an empty string. If the entire command is one or more terms which together produce an empty string, then the bot will not send any response.

## Advanced Examples

Multi-stream link based on service:

```
[MaddiieManeater] !command set !multi [[equal{{[[service]]}}{{Twitch}}{{Watch [[foreach{{}}{{[[ifarg2{{, }}]]}}]] and me at the same time! example.com/multistream/[[channel]]/[[foreach.lower{{}}{{/}}]]}}{{Beam has not implemented their own multi-streams as of 2015/07/19. Sorry.}}]]
[OTB] Set command '!multi'.

<On Twitch in MaddiieManeater's channel>
[MaddiieManeater] !multi NthPortal
[OTB] Watch NthPortal and me at the same time! example.com/multistream/maddiiemaneater/nthportal/
[MaddiieManeater] !multi NthPortal The_Lone_Devil
[OTB] Watch NthPortal, The_Lone_Devil, and me at the same time! example.com/multistream/maddiiemaneater/nthportal/the_lone_devil/

<On Beam in MaddiieManeater's channel>
[MaddiieManeater] !multi NthPortal The_Lone_Devil
[OTB] Beam has not implemented their own multi-streams as of 2015/07/19. Sorry.
```

A command which only works for one person:

```
[NthPortal] !command set !example [[equal{{[[user]]}}{{maddiiemaneater}}{{Hi Maddiie!}}]]
[OTB] Set command '!example'.

[NthPortal] !example

[MaddiieManeater] !example
[OTB] Hi Maddiie!
```

{% endraw %}
