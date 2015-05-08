---
title: Chat Documentation
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: How to Make the Bot Do Things

## Table of Contents

## Version

Version 1.0 [WIP]

### Changelog
* 1.0

## Background

There are a few terms which will be useful to understand before discussing how to use them in chat.

### Commands

Commands are words which the bot will respond to if they are the first word in a message. Commands often start with an exclamation mark, such as `!example`, but they can be any string of characters without a space in them.

### Aliases

An alias is a word which represents another word or group of words. Like commands, aliases are only processed by the bot if they are the first word of a message. However, an alias can expand into a command and parameters (other text after the command) for the command, to make running certain commands easier. If an alias expands to something which is not a command or another alias, it won't do anything.

For example, `!addcom` is said to be "aliased" to `!command add` because if you type `!addcom !example example response`, `!addcom` will be replaced by `!command add`, making it as if you had typed `!command add !example example response`. An alias will sometimes be denoted as `<alias>='<expansion>'`. In this example, `!addcom='!command add'`.

A given alias will not be processed more than once per message. What does that mean? Suppose you have two aliases, `!alias-1='!alias-2 and then some parameters'` and `!alias-2='!alias-1'`. If someone types `!alias-1` in chat and the bot processes it, it will replace `!alias-1` with `!alias-2 and then some parameters`, and then in turn replace that with `!alias-1 and then some parameters`. However, it will stop there, and will not replace `!alias-1` with its corresponding text again in that message. If `!alias-1` is also a command, it will be run; otherwise, nothing will happen.

## Adding Your Own Commands




{% endraw %}
