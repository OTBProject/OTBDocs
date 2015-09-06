---
title: Tutorial - Repeating Commands
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: Repeating Commands Periodically

## Table of Contents

- [Version](#version)

## Version

1.0

## Introduction

If you want to have a command repeat periodically (say, every 10 minutes), you can do so using the `!repeat` command.

To have multiple commands run repeatedly, but at different times, you have a few options:

 - You can add the repeats at different times, so that the intervals will not match up.
   Disadvantage: when the bot restarts (or leaves and rejoins the channel), all of the repeats will run at the same time.

 - You can add the repeats and specify an offest. For example, with an offset of 4 minutes and an interval of 10 minutes, it will repeat every 10 minutes starting 4 minutes from now.
   Disadvantage: you have to add all of the repeats at practically the same moment (or the repeats will be offset from each other differently when the bot restarts).

 - You can have the repeat interval and offset be based on the beginning of each hour, rather than based on the time it is added. Then, with an interval of 10 minutes, an offset of 4 minutes, and starting at 10 o'clock, it will run at 10:04, 10:14, 10:24, etc., until it resets at the start of the next hour (11 o'clock).
   Disadvantage: intervals which are not even factors of 60 minutes (e.g. 13 minutes) will have their last interval of each hour shortened.

## Syntax for Adding Repeats

The basic command to have a command repeat periodically is `!repeat <subcommand> <flags> <interval> <offset> <command>`. (Example: `!repeat add --no-reset 10 5 !example-command with arguments`.)


 - `<subcommand>` can be `add`, `new`, `set`, or `edit`; see [below](#adding-or-setting-a-repeat)
 - `<flags>` are optional and change whether or not the repeat resets hourly, and what time units are used; they will be discussed [shortly](#flags)
 - `<interval>` and `<offset>` are non-negative integers
 - `<command>` is the command to be repeated, with or without accompanying arguments (it may contain spaces)

#### Flags

Flags are optional, and their order is not significant. All flags begin with `--`.

By default, a repeat will [reset hourly](#hourly-reset). If you [do not wish](#no-reset) it to do so, you can use the flag `--no-reset`. The flag `--reset` will make it reset hourly (which it would have anyway, since that is the default behaviour), but is not needed. `--reset` and `--no-reset` are mutually exclusive (cannot both be used in the same command).

By default, the values given for `<interval>` and `<offset>` are evaluated in minutes. The flags `--seconds` and `--hours` can be used to instead evaluate both `<interval>` and `<offset>` in seconds or hours, respectively. The flag `--minutes` will make those values be evaluated in minutes (which they would have been anyway, since that is the default behaviour), but is not needed. `--seconds`, `--minutes`, and `--hours` are mutually exclusive.

(`--reset` and `--minutes` are not strictly needed, but are valid flags for reasons of consistency, and may also potentially be used make the meaning of the command more obvious.)

#### Adding or Setting a Repeat

To add a repeated command only if that command (with the same arguments) is not already set to repeat, use one of the following commands:

 - `!repeat add <flags> <interval> <offset> <command>`
 - `!repeat new <flags> <interval> <offset> <command>`

To set a repeated command even if that command (with the same arguments) is already set to repeat (and overwrite the previous interval and offset if it is), use one of the following commands:

 - `!repeat set <flags> <interval> <offset> <command>`
 - `!repeat edit <flags> <interval> <offset> <command>`

#### Hourly Reset

#### No Reset

## Removing a Repeat

## Disabling a Repeat

## Listing Repeats

{% endraw %}
