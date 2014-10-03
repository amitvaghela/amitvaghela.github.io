---
layout: post
title: "NSUserDefaults Data and iOS8 Simulator"
date: 2014-10-03 22:29:30 +1000
comments: true
categories:
---

This is a new behaviour I've noticed in iOS 8 simulator that deleting applications from simulator no longer deleting data stored in NSUserDefaults. Not quite sure it's a bug or a feature.

You can reset content and setting in simulator but if you don't want to do it then you can delete the application from simulator and then delete the plist file from,

{% codeblock %}
Macintosh HD ▸ Users ▸ username ▸ Library ▸ Developer ▸ CoreSimulator ▸ Devices ▸ SimulatorCrypticNumber ▸ data ▸ Library ▸ Preferences ▸ YourApplicationBundleID.plist
{% endcodeblock %}

In the Devices folder you'll see folder for each simulator, check deviceType in device.plist to check which simulator folder it is.

If you are like me who don't want to remember the location then you can create a shortcut in your sidebar for that location.
