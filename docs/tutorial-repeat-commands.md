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
   Disadvantage: you have to add all of the repeats at practically the same moment (or the repeats will be offset from each other differently when the bot restarts)

 - You can have the repeat interval and offset be based on the beginning of each hour, rather than based on the time it is added. Then, with an interval of 10 minutes, an offset of 4 minutes, and starting at 10 o'clock, it will run at 10:04, 10:14, 10:24, etc., until it resets at the start of the next hour (11 o'clock).
   Disadvantage: intervals which are not even factors of 60 minutes (e.g. 13 minutes) will have their last interval of each hour shortened.

## Basic Syntax

## Hourly Reset

## No Reset

## Disabling a Repeat

{% endraw %}
