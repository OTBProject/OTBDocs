---
title: Web Documentation
layout: markdown
---

{% raw %}
# OTB Project Documentation

### Using the Web Interface

## Table of Contents

- [Version](#version)
	- [Changelog](#changelog)
- [Opening](#opening)
- [Read Only](#read-only)
- [Writable](#writable)

## Version

Version 0.1.0

### Changelog
* 0.1.0

## Opening

### On the local machine
If you are trying to open the web interface on the machine that the bot is running on, providing that you have the GUI open, there is a button to open the web interface in the default web browser.
If you do not have the GUI open, or want to open it in a different browser, you can navigate to <a href="http://localhost:22222" target="_blank">http://localhost:22222</a> by default to view a read only version and <a href="http://127.0.0.1:22222" target="_blank">http://127.0.0.1:22222</a> by default to view the writable version.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>.

### On A Remote Machine

#### The Same Network

If you are trying to open the web interface from the local network you will want to navigate to &lt;local IP Address of the server&gt;:22222 (for example 192.168.1.2:22222) by default to view the whichever version the IP address of the machine you are on is allowed to see.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>.

#### Over The Internet

If you are trying to open the web interface from across the internet you will want to navigate to &lt;public IP Address of the server&gt;:22222 (for example 137.183.92.180:22222) by default to view the whichever version the public IP address of the machine you are on is allowed to see.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>.

## Read Only

The read only version of the web interface is what the majority of people will see. It allows them to look at the commands, aliases, and quotes for any channel that the bot may be in. Commands are split into the different execution user levels, as well as all commands that a person of a certain user level may execute.

Upon [opening](#opening) the web interface you will want to choose the channel, a drop down will appear where you will choose between quotes, aliases and the command execution levels.

### Commands

### Aliases

### Quotes

## Writable

The writable version of the web interface is what is available to people with IP addresses that match those specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>. By default all private IP addresses are white listed. As far as the displaying of information it is the same as the [read only](#read-only) version. 

### Add new

#### Commands
1. Navigate to one of the commands pages.
2. Click the "New" button.
3. In the pop up specify the command name and other details.
4. Hit save.

#### Aliases
Not yet implemented

#### Quotes
Not yet implemented

### Modify

#### Commands
1. Navigate to the command.
2. Click the "Edit" button for that command.
3. In the pop up make the changes.
4. Hit save.

#### Aliases
Not yet implemented

#### Quotes
Not yet implemented

### Delete

#### Commands
1. Navigate to the command.
2. Click the dropdown next to the "Edit" button for the command.
3. Click "Delete".
4. Check the checkbox.
5. Click the "Delete" Button.

#### Aliases
Not yet implemented

#### Quotes
Not yet implemented

### Disable

#### Commands
1. Navigate to the command.
2. Click the dropdown next to the "Edit" button for the command.
3. Click "Disable".

#### Aliases
Not yet implemented

#### Quotes
Not yet implemented


{% endraw %}
