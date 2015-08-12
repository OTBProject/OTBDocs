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
- [Writeable](#writeable)

## Version

Version 0.1.0

### Changelog
* 0.1.0

## Opening

### On the local machine
If you are trying to open the web interface on the machine that the bot is running on, providing that you have the GUI open, there is a button to open the web interface in the default web browser.
If you do not have the GUI open, or want to open it in a different browser, you can navigate to <a href="http://localhost:22222" target="_blank">http://localhost:22222</a> by default to view a read only version and <a href="http://127.0.0.1:22222" target="_blank">http://127.0.0.1:22222</a> by default to view the writable version.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>

### On A Remote Machine

#### The Same Network

If you are trying to open the web interface from the local network you will want to navigate to <local IP Address of the server>:22222 (for example 192.168.1.2:22222) by default to view the whichever version the IP address of the machine you are on is allowed to see.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>

#### Over The Internet

If you are trying to open the web interface from across the internet you will want to navigate to <public IP Address of the server>:22222 (for example 137.183.92.180:22222) by default to view the whichever version the public IP address of the machine you are on is allowed to see.
The port number at the end of the URL will be whatever is specified in the <a href="config-documentation.md#web-config" target="_blank">config</a>

## Read Only

## Writeable

{% endraw %}
