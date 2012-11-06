---
layout: post
title: "Installing rspec in rails app"
date: 2012-11-06 17:54
comments: true
categories: installation
published: true 
---

Support TDD within your rails app by using rspec.

Add to **Gemfile**
{% codeblock [Gemfile] [lang:Ruby] %}
group :test do
  gem 'rspec-rails'
end
{% endcodeblock %}

Enter in Terminal in your **app_folder**
{% codeblock %}
rails g rspec:install
{% endcodeblock %}