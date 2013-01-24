---
layout: post
title: "How to move your Octopress Blog to a new Mac"
date: 2013-01-22 12:07
comments: true
categories: 
published: false 
---

My blog of choice as of right now is Octopress. And it needs to move to my new Mac as well. Octopress requires Ruby, which I haven't yet installed on my machine. Read about my experience with configuring your new Mac [here](). 

<!-- more -->

## Before you begin  
1. Install [Git]() 
2. Install [Ruby]()

## Move your blog
In your Terminal, choose a folder to host your blog content. Read [here]() on suggested folder structure.

```
git clone git://github.come/YOUR_OCTOPRESS_REPO
cd octopress
ruby --version
```

Install any dependencies.
```
gem install bundler
bundle install
```