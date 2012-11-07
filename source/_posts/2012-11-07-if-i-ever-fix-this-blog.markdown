---
layout: post
title: "If I ever fix this blog"
date: 2012-11-07 00:46
comments: true
categories: 
published: true 
---

Debugging

If you are reading this post, I was able to save this blog and debug this #$!#%#%)&$ error. Pardon my french.

<!-- more -->

When running octopress
{% codeblock %}
rake preview
{% endcodeblock%}

the followng error showed up:

{% codeblock %}
127.0.0.1 - - [06/Nov/2012 19:06:16] "GET /stylesheets/screen.css HTTP/1.1" 200 42533 0.0037
127.0.0.1 - - [06/Nov/2012 19:06:16] "GET /images/line-tile.png?1352246753 HTTP/1.1" 200 636 0.0027
127.0.0.1 - - [06/Nov/2012 19:06:16] "GET /images/rss.png?1352246753 HTTP/1.1" 200 490 0.0025
127.0.0.1 - - [06/Nov/2012 19:06:16] "GET /images/noise.png?1352246753 HTTP/1.1" 200 17742 0.0141
127.0.0.1 - - [06/Nov/2012 19:06:18] "GET /stylesheets/screen.css HTTP/1.1" 304 - 0.0011
[2012-11-06 19:06:18] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET / HTTP/1.1" 304 - 0.0013
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /stylesheets/screen.css HTTP/1.1" 304 - 0.0011
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/github.js HTTP/1.1" 304 - 0.0011
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/octopress.js HTTP/1.1" 304 - 0.0016
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/modernizr-2.0.js HTTP/1.1" 304 - 0.0014
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/ender.js HTTP/1.1" 304 - 0.0011
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/twitter.js HTTP/1.1" 304 - 0.0009
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /javascripts/libs/jXHR.js HTTP/1.1" 304 - 0.0020
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:19] "GET /images/Wind_Map.jpg HTTP/1.1" 304 - 0.0122
[2012-11-06 19:06:19] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:25] "GET / HTTP/1.1" 304 - 0.0012
[2012-11-06 19:06:25] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
127.0.0.1 - - [06/Nov/2012 19:06:25] "GET /stylesheets/screen.css HTTP/1.1" 304 - 0.0012
[2012-11-06 19:06:25] WARN  Could not determine content-length of response body. Set content-length of the response or set Response#chunked = true
{% endcodeblock %}

After several attempts at googling it, numerous pulls and pushs and rebase commands, I decided to get to the very bottom of it
Locate file
{% codeblock %}
~/.rvm/rubies/ruby-1.9.3-p0/lib/ruby/1.9.1/webrick/httpresponse.rb
{% endcodeblock %}

Set and set it to **true**
{% codeblock [httpresponse.rb] [lang:Ruby] %}
53 @chunked = true
{% endcodeblock %}

This should get rid of your error.
