---
layout: post
title: "Homebrew Install growlnotify on Snow Leopard and Lion"
date: 2012-05-01 00:51
comments: true
categories: MacOSX
tags: MacOSX
---

Currently homebrew already removed formula of growlnotify. If you want to use the Gem [growl][gl] with a well-known app growlnotify and you may encounter this error with Growlnotify on Snow Leopard:

	dyld: Symbol not found: _kSecRandomDefault
	  Referenced from: /usr/local/bin/growlnotify
	  Expected in: /System/Library/Frameworks/Security.framework/Versions/A/Security
	 in /usr/local/bin/growlnotify
	Trace/BPT trap

<!--more-->

Here are the formulas:


### For Snow Leopard with growlnotify v1.2.2

	brew install https://raw.github.com/mxcl/homebrew/bd40f1e5f89fad962b021c827d56a9fdea0c847d/Library/Formula/growlnotify.rb


### For Lion with growlnotify v1.3

	brew install https://raw.github.com/mxcl/homebrew/15d6da0023924969fa6ad8a7cf743c4b39838e6e/Library/Formula/growlnotify.rb


Alternatively you could try on their [offical download page][gl-down]

[gl]:http://rubygems.org/gems/growl
[gl-down]:http://growl.info/downloads


