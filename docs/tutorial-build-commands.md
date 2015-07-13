---
title: Tutorial - Building Commands
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: Building Commands

## Table of Contents

- [Version](#version)

## Version

1.0

## Overview

This tutorial is about how to make commands which are more than a simple, unchanging sentence. It will describe how to build commands which include the name of the person running the command, an argument provided to the command, and much more.

Special terms are used to specify a value which may vary across the different times a command is run.

There is an index of all terms and a short description of each at the end of the tutorial, for reference.

## `user`

One of the simplest terms is `[[user]]`, which refers to the user who ran the command. For example, if there is a command `!example` with the response `[[user]] ran this command`, then if the user `NthPortal` runs the command `!example`, the bot will send the message `nthportal ran this command`. If `The_Lone_Devil` runs the command, it will print `the_lone_devil ran this command`.

The user's name is always given entirely in lowercase.

## Terms and their Structure

Having seen an example of a term, we will now look at the structure of terms in general. The general structure of any term is:

```
[[term.modifier{{embedded string}}]]
```

but it may be as simple as:

```
[[term]]
```

That may seems somewhat confusing and unclear, but will hopefully be less so after we break it down.

* All terms are enclosed by `[[` and `]]`. If either of these are used in a command not in the context of a term, other terms in the command's response will not be processed properly or at all.
* A term may optionally be followed by a `.` and a modifier. Modifiers will be discussed [shortly](#modifiers).
* A term may optionally be followed by one or more 'embedded strings'. Embedded strings follow the modifier if it is present, or the term if there is no modifier. Each embedded string is enclosed by `{{` and `}}`. Embedded strings will be discussed in detail [later](#embedded-strings), but for now, think of them as a way to provide extra information to the term.
* With the exception of embedded strings, no spaces are allowed in a term (inside of `[[` and `]]`).

## Modifiers

A modifier allows you to customize the the result of a term, and is best explained by an example.

As you saw earlier, the `[[user]]` term always gets the user's name entirely in lowercase. If you want the user's name to be entirely in uppercase, you would use the modifier `upper`. If we modify the previously mentioned `!example` command slightly, such that its response is `[[user.upper]] ran this command`, then when NthPortal runs it, the bot will respond with `NTHPORTAL ran this command`.

The valid modifiers and their descriptions are listed in the table below. They are case sensitive. If an invalid modifier (one not specified below) is given, it is ignored.

(Note: The word or words being modified are referred to as 'the string'.)

| Modifier | Description |
|:---------|:------------|
|`lower`|The string is made entirely lowercase.|
|`upper`|The string is made entirely uppercase.|
|`first_cap`|The first letter of the string is made uppercase. All other letters are made lowercase.|
|`word_cap`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are made lowercase.<br>Identical to `first_cap` for anything which is a single word (e.g. `[[user]]`).|
|`first_cap_soft`|The first letter of the string is made uppercase. All other letters are not changed.|
|`word_cap_soft`|The first letter of each word (separated by a space) in the string is made uppercase. All other letters are not changed.<br>Identical to `first_cap_soft` for anything which is a single word (e.g. `[[user]]`).|

## `count`

Another simple term is the term `[[count]]`. 

## Index

{% endraw %}
