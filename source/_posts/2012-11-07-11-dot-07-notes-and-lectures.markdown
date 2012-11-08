---
layout: post
title: "Nov07 notes and lectures"
date: 2012-11-07 10:44
comments: true
categories: 
published: false 
---

rspec --format documentation
rake spec:models

###rspec methods:

.to_sentence(options ={})
  action view helper method

###Steps: 

git clone git@github.com:innatewonderer/mixtapeapp.git
 add origin master 
git remote add upstream git@github.com:flatiron-school/mixtapeapp.git
git fetch upstream
git merge upstream/master

Guard Rspec
    install guard /=> https://github.com/guard/guard#readme
    add too gemfile
    add gem terminal-notifier-guard for last version of Mac
      group :development do
        gem 'guard-rspec'
        gem 'terminal-notifier-guard'
      end

rails g model Album name:string
rake db:migrate

rake spec

guard

### GitTip:

Git BRANCH

  git co -b guard-rspec-2


###Ideas:

Setup Scrapes
  Setup first development environment

Rails templates
  to include all of the gems you want installed when run rails setup

###Resources: 

Capybara with Rspec
  fills forms for you
  watch rails casts #257
  #155 for cucumber
  #187 integration testing

Thoughtbot
  check Suspenders

