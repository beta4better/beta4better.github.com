---
layout: post
title: "Using socks5 proxy for Chromium"
date: 2012-03-05 21:33
categories: [socks5, proxy, chromium]
tags: [socks5, proxy, chromium]
---

Why I use proxy for a browser? As you know in China, the GFW block some really nice site, such as [twitter](http://twitter.com/), [facebook](http://facebook.com/) and even [google](http://google.com/), so proxy or VPN is really needed. For VPN, I do not really need, I just want to browse some sites some times, so a proxy is enough.

In [Chromium](http://code.google.com/intl/en/chromium/) option, there's a button to set the proxy, but it not works, error show as following: 

> When running Chromium under a supported desktop environment, the system proxy settings will be used. However, either your system is not supported or there was a problem launching your system configuration.
> 
> But you can still configure via the command line. Please see man chromium-browser for more information on flags and environment variables.

So I need to launch the Chromium with this command: 

    chromium-browser --proxy-server=socks5://127.0.0.1:10000

Then is works.

Enjoy the internet.