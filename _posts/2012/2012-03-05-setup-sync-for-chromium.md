---
layout: post
title: "Setup sync for Chromium"
date: 2012-03-05 21:54
categories: [chromium, sync, google, chrome]
tags: [chromium, sync, google, chrome]
---

As [Chromium](http://code.google.com/intl/en/chromium/)  sync says: 

> Chromium syncs your data with your Google account securely. Keep everything synced or choose what data to sync from this computer.

But sync comes with the following error: 

    The sync server is busy, please try agsin later.

I tried several times, each time I try the same error comes, so I decide to switch [Chromium](http://code.google.com/intl/en/chromium/)  to [Chrome](http://www.google.com/chrome). You may download it here for b4bit version.

* [https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb](https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb)

Then install the deb file with the following command: 

    dpkg -i google-chrome-stable_current_amd64.deb

Two screen shot for [Google Chrome](http://www.google.com/chrome), sync works, everything synced.

<img src="/assets/images/2012/03/google-chrome-sync.png" width="480px" />

<img src="/assets/images/2012/03/google-chrome-getting-started.png" width="480px" />