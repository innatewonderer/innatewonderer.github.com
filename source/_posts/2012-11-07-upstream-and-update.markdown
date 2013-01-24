---
layout: post
title: "Upstream and update"
date: 2012-11-07 17:49
comments: true
categories: 
published: true 
---

You forked something, cloned it to your machine, but didn't setup remote connection to the origin repository.

{% codeblock %}
git remote add upstream *url to original repository*
git fetch upstream
git merge upstream/master
{% endcodeblock %}

