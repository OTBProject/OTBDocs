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
  - [user](#user)
  - [count](#count)
  - [args](#args)

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
For example, if there was a term `[[example]]` which got replaced by the string `this is an example`, then `[[example.upper]]` would get replaced by `THIS IS AN EXAMPLE`. (Please note that `[[example]]` is not actually a term.)

The valid modifiers and their descriptions are listed in the table below. They are case sensitive. If an invalid modifier (one not specified below) is given, it is ignored.

| Modifier | Description |
|:---------|:------------|
|`lower`|The string is made entirely lowercase.|
|`upper`|The string is made entirely uppercase.|
|`first_cap`|The first letter of the string is made uppercase. All other letters are made lowercase.|
|`word_cap`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are made lowercase.<br>Identical to `first_cap` for anything which is a single word.|
|`first_cap_soft`|The first letter of the string is made uppercase. All other letters are not changed.|
|`word_cap_soft`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are not changed.<br>Identical to `first_cap_soft` for anything which is a single word.|

Modifiers can be used for any term. There are certain terms for which modifiers have no effect, but even in those cases they do no harm.

## Embedded Strings

An embedded string is a string enclosed in `{{` and `}}` which provides extra information to a term. For example, it might provide a default value for the term if some other value is missing. Embedded strings are necessary, especially for more advanced terms, to allow greater functionality.

Unlike the rest of the term, an embedded string may contain spaces, and may even contain other terms. They may also be empty `{{}}` if you so desire.

If a term expects more embedded strings than you've given it, it will treat any missing embedded strings as empty. For example, if you use the term `[[example{{string 1}}{string 2}}]]`, but the term `[[example]]` uses three embedded strings, it will treat the third embedded string as empty; that is, it will be as if you had used the term as `[[example{{string 1}}{{string 2}}{{}}]]`.

## Terms

| Term | Description |
|:-----|:------------|
|`[[user]]`|Returns the name of the user who ran the command.|
|`[[bot]]`|Returns the bot's username.|
|`[[channel]]`|Returns the channel in which the command was run.|
|`[[service]]`|The name of the service the bot is connected to ("Twitch" or "Beam").|
|`[[count]]`|The number of times the command has been run since it was created or since it was last modified.|
|`[[numargs]]`|The number of arguments with which the command was run.|
|`[[args{{default}}]]`|All arguments with which the command was run (separated by spaces). If the command is run without arguments, and a default is given, the default is used. The default can contain another special term. If no default is given, it is replaced by an empty string (it is left blank).|
|`[[argN{{default}}]]`|The `N`th argument, where `N` is a whole number greater than 0. If the command is run with fewer than `N` arguments, and a default is given, the default is used. The default can contain another special term. If no default is given, it is replaced by an empty string (it is left blank).|
|`[[fromargN{{default}}]]`|All the arguments from the `N`th argument and on. As with `[[argN]]`, `N` must be a whole number. If `N` is 1, it is equivalent to `[[args]]`.|
|`[[quote]]` or `[[quote{{id}}]]`|A random quote from the quote database if no ID is given. If an ID is given, the quote with the specified ID (if it exists; an empty string if it does not exist or the ID is invalid).|
|`[[ifargs{{yes_args}}{{no_args}}]]`|Prints the first embedded string string if at least one argument was given. If no arguments were given, it prints the second embedded string. For either condition, if no string is supplied, it does nothing.|
|`[[ifargN{{N_args}}{{not_N_args}}]]`|Prints the first embedded string if at least `N` arguments were given. If less than `N` arguments were given, it prints the second embedded string. For either condition, ff no string is supplied, it does nothing. `N` must be greater than 0.|
|`[[foreach{{prepend}}{{append}}]]`|For each argument provided, prints the string specified as `prepend`, the argument, and then the string specified as `append`. If a modifier (described later) is used, it is applied to each argument (but not to `prepend` or `append`). If only one string is provided, it is `prepend`. If both are left out, the arguments are printed unmodified (and without spaces).|
|`[[equal{{compare1}}{{compare2}}{{same}}{{different}}]]`|If the first two embedded strings are the same, then it prints the third embedded string. If not, it prints the fourth embedded string. Not particularly useful if neither of the first two embedded strings are a term.|

#### `user`

One of the simplest terms is `[[user]]`, which refers to the user who ran the command. For example, if there is a command `!example` with the response `[[user]] ran this command`, then if the user `NthPortal` runs the command `!example`, the bot will send the message `nthportal ran this command`. If `The_Lone_Devil` runs the command, it will print `the_lone_devil ran this command`.

When the command is run, the term `[[user]]` is replaced by the user's name. The user's name is always given entirely in lowercase.

#### `count`

Another simple term is the term `[[count]]`, which is replaced by the number of times the command has been run.

For example, take a command `!example` with the response `This command has been run [[count]] times`. If it has already been run 9 times, then the next time it is run, the response will be `This command has been run 10 times`.

Though a modifier can be used with `[[count]]`, it has no effect because `[[count]]` is replaced by a number made up of digits, which do not have uppercase and lowercase versions.

#### `args`



{% endraw %}
