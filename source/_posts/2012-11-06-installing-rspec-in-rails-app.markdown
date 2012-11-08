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


class Album < ActiveRecord::Base
  attr_accessible :name, :artist_name, :song_names
  belongs_to :artist
  has_many :songs

  def artist_name
    artist.name if artist_name
  end

  def artist_name=(string)
    artist = Artist.find_or_create_by_name(string)
  end
end