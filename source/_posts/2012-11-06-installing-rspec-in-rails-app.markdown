---
layout: post
title: "Installing rspec in rails app"
date: 2012-11-06 17:54
comments: true
categories: installation
published: false 
---

## Support TDD within your rails app by using rspec.

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

##Using Guard with Rspec
After following careful instructions from their [GitHubPage](https://github.com/guard/guard-rspec), run this before running **guard**
{% codeblock %}
rake spec
{% endcodeblock %}
It will reset your tables.

Else :
  rake db:reset

$rails generate rspec:install
      create  .rspec
      create  spec
      create  spec/spec_helper.rb

rake db:test:prepare
  When want to start testing in your rails app
  