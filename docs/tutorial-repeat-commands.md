---
title: Tutorial - Repeating Commands
layout: markdown
---

{% raw %}

# OTB Project Documentation

### Tutorial: Repeating Commands Periodically

## Table of Contents

- [Version](#version)
- [Overview](#overview)
- [Adding a Repeat](#adding-a-repeat)
  - [Syntax](#syntax)
  - [Flags](#flags)
  - [Adding or Setting a Repeat](#adding-or-setting-a-repeat)
  - [Hourly Reset](#hourly-reset)
  - [No Reset](#no-reset)
- [Removing a Repeat](#removing-a-repeat)
- [Disabling a Repeat](#disabling-a-repeat)
- [Listing Repeats](#listing-repeats)

## Version

1.0

## Overview

If you want to have a command repeat periodically (say, every 10 minutes), you can do so using the `!repeat` command.

To have multiple commands run repeatedly, but at different times, you have a few options:

 - You can add the repeats at different times, so that the intervals will not match up.
   Disadvantage: when the bot restarts (or leaves and rejoins the channel), all of the repeats will run at the same time.

 - You can add the repeats and specify an offset. For example, with an offset of 4 minutes and an interval of 10 minutes, it will repeat every 10 minutes starting 4 minutes from now.
   Disadvantage: you have to add all of the repeats at practically the same moment (or the repeats will be offset from each other differently when the bot restarts).

 - You can have the repeat interval and offset be based on the beginning of each hour, rather than based on the time it is added. Then, with an interval of 10 minutes, an offset of 4 minutes, and starting at 10 o'clock, it will run at 10:04, 10:14, 10:24, etc., until it resets at the start of the next hour (11 o'clock).
   Disadvantage: intervals which are not even factors of 60 minutes (e.g. 13 minutes) may have their last interval of each hour shortened.

## Adding a Repeat

### Syntax

The basic command to have a command repeat periodically is `!repeat <subcommand> <flags> <interval> <offset> <command>`. (Example: `!repeat add --seconds --no-reset 450 300 !example-command with arguments`.)

 - `<subcommand>` can be `add`, `new`, `set`, or `edit`; see [below](#adding-or-setting-a-repeat).
 - `<flags>` are optional and change whether or not the repeat resets hourly, and what time units are used; they will be discussed [shortly](#flags).
 - `<interval>` is a non-negative integer specifying the amount of time between each execution of the command.
 - `<offset>` is a non-negative integer specifying the offset (from the beginning of each hour or from when the repeat is added; see [here](#hourly-reset) and [here](#no-reset)) before the command is run the first time. It can be larger than `<interval>`, although it usually will not be. A value of `0` means no offset.
 - `<command>` is the command to be repeated, with or without accompanying arguments (it may contain spaces). It may be an alias as well.

### Flags

Flags are optional, and their order is not significant. All flags begin with `--`.

By default, a repeat will [reset hourly](#hourly-reset). If you [do not wish](#no-reset) it to do so, you can use the flag `--no-reset`. The flag `--reset` will make it reset hourly (which it would have anyway, since that is the default behaviour), but is not needed. The flags `--reset` and `--no-reset` are mutually exclusive (cannot both be used in the same command).

By default, the values given for `<interval>` and `<offset>` are evaluated in minutes. The flags `--seconds` and `--hours` can be used to instead evaluate both `<interval>` and `<offset>` in seconds or hours, respectively. The flag `--minutes` will make those values be evaluated in minutes (which they would have been anyway, since that is the default behaviour), but is not needed. The flags `--seconds`, `--minutes`, and `--hours` are mutually exclusive.

*Note: `--reset` and `--minutes` are not strictly needed, but are valid flags for reasons of consistency, and may also potentially be used make the behaviour of the command more obvious.*

For the remainder of this tutorial, it is assumed that `<interval>` and `<offset>` are in minutes unless otherwise noted.

### Adding or Setting a Repeat

To add a new repeated command, use one of the following commands *(Note: this doesn't work if that command with the same arguments is already set to repeat)*:

 - `!repeat add <flags> <interval> <offset> <command>`
 - `!repeat new <flags> <interval> <offset> <command>`

To set a repeated command even if that command (with the same arguments) is already set to repeat, use one of the following commands *(Note: if it is already set to repeat, this will overwrite the previous interval and offset)*:

 - `!repeat set <flags> <interval> <offset> <command>`
 - `!repeat edit <flags> <interval> <offset> <command>`

### Hourly Reset

If a repeat is made to reset every hour, then the offset is from the beginning of each hour. That means, starting `<offset>` minutes after the beginning of each hour, the command will be run every `<interval>` minutes.

For example, suppose a repeat is added with an offset of 5 minutes and an interval of 10 minutes. It will run at `:05`, `:15`, `:25`, `:35`, `:45` and `:55` of each hour (for 10 o'clock, `:05` is `10:05`). However, a repeat with an offset of 0 minutes and an interval of 10 minutes will run at `:00`, `:10`, `:20`, `:30`, `:40` and `:50` of each hour.

Both of the previous examples had 10 minute intervals - an interval length which evenly divides an hour. An interval length which does not evenly divide an hour, however, may have its final interval of each hour cut short. For example, suppose a repeat is added with an offset of 0 minutes and an interval of 13 minutes. It will run at `:00`, `:13`, `:26`, `:39` and `:52` of each hour. The final interval of the hour is only 8 minutes (rather than 13), as it will be run at `:00` of the following hour.

### No Reset

If a repeat is not made to reset every hour, then the offset is from the time it is added, or from when the bot rejoins the channel (if it restarts or leaves). That means, starting `<offset>` minutes after the repeat is added (or after the bot rejoins the channel), the command will be run every `<interval>` minutes.

## Removing a Repeat

To remove a repeat, use the command `!repeat remove <command>`. `<command>` must be the full command as you added it, including arguments. You can also use one of the following commands:

- `!repeat delete <command>`
- `!repeat rm <command>`
- `!repeat del <command>`

## Disabling a Repeat

Though it is not possible to disable a repeat itself, disabling the command (or alias) which is set to repeat will prevent anything from happening when it is run.

## Listing Repeats

You can list all the repeated commands using `!repeat list`.

{% endraw %}
