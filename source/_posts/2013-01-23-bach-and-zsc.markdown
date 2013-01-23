---
layout: post
title: "Bash and ZSC"
date: 2013-01-23 12:40
comments: true
categories: 
published: true 
---

As I've been struggling with setting up my new Mac to be proper RoR utility I need it to be, I can across [Laptop](https://github.com/thoughtbot/laptop) script that took care of most installation work for me. It did prompt me to switch to `zsh`. 

For reasons yet unknown to me, `zsh` doesn't follow instructions in `.bash_profile`. And I like my aliases and prompt line settings, so I'm going to switch it back to `bash`
  
{% codeblock %}
exec bash
{% endcodeblock %}

When I figure out what is the power of `zsh` and would like to switch back to it:

{% codeblock %}
exec zsh
{% endcodeblock %}

