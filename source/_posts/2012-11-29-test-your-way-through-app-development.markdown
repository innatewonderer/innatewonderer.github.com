---
layout: post
title: "Testing Tools in Rails Application Development"
date: 2012-11-29 16:41
comments: true
categories: 
published: true 
---

Did you ever wake up and thought "Today, I'm going to write the entire app in one attempt"? How did it go for you?

One of the hardest thing for me while learning coding was to understand what my lines of code actually do. I would write ten lines of code only to see it do nothing, and have no idea where to start debugging it. I would assume my entire logic was incorrect, erase it all only to find out later that I used `.each` instead of `.map`.

<!-- more -->

My biggest AHA moment was to discover tools available to test what my code does as I develop my functionalities. Let's take a look at few examples I cannot imagine my day without.

### Use Irb to Master Ruby ###

Run `irb` in your console to access Interactive Ruby console. Can't figure out if you need to use `.map` or `.each` Test it.

{% codeblock [brainpickings-scraper.rb] %}
[17:50:06] (master) brainpickings-scraper
$ irb
001:0 > var = [1, 2, 3]
=> [1, 2, 3]
002:0 > var.each {|i| i+i}
=> [1, 2, 3]
003:0 > var.map {|i| i+i}
=> [2, 4, 6]
{% endcodeblock %}

Ohhh, now it makes sense. My `.each` returns the original value, and `.map` returns the outcome. Easy!

### "Puts" in Ruby ###

Nokogiri scraper goes through the page and collects values that you can store in the database for later use in the application. Simplified version of my personal scraper project looked like this:

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}

require 'nokogiri'
require 'open-uri'
require 'sqlite3'
require 'FileUtils'

FileUtils.rm("books.db") if File.exists?("books.db")

db = SQLite3::Database.new "books.db"

db.execute <<-SQL
  CREATE TABLE books (
    id INTEGER PRIMARY KEY,
    title TEXT,
  );
SQL

books_url = "http://bookpickings.brainpickings.org/"
doc = Nokogiri::HTML(open(books_url))
books = doc.css(".photo")

books.each do |book|
  title = book.at_css(".post_title h1")

  db.execute("INSERT INTO books (title) 
                VALUES (?)", title)
end

{% endcodeblock %}

Run this file in your Console to see the result:

{% codeblock [brainpickings-scraper.rb] %}
[16:47:26] (updated) bookshelf-static
$ ruby brainpickings-scraper.rb
{% endcodeblock %}

It might or might NOT show lines that look like this:

{% codeblock [brainpickings-scraper.rb] [lang: Ruby]%}
/Users/jenya/.rvm/gems/ruby-1.9.3-p194/gems/sqlite3-1.3.6/lib/sqlite3/statement.rb:41:in `bind_param': can't prepare Nokogiri::XML::Element (RuntimeError)
  5/lib/nokogiri/xml/node_set.rb:238:in `each'
  from brainpickings-scraper.rb:25:in `<main>'
{% endcodeblock %}

We got an error. (Surprised? Don't be). Let's start debugging.
I'm going to comment out the call to the database and ask `ruby` to print the value of `title` on the screen.

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}
books_url = "http://bookpickings.brainpickings.org/"
doc = Nokogiri::HTML(open(books_url))
puts 
books.each do |book|
   puts title = book.at_css(".post_title h1")

#   db.execute("INSERT INTO books (title) 
#                 VALUES (?)", title)
end
{% endcodeblock %}

This will return:

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}
<h1>Sketchbooks: The Hidden Art of Designers, Illustrators, and Creatives</h1>
{% endcodeblock %}
What does this tell us? **Too much information!!!** Let's refactor our code to only return the text from the `title` tag.

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}
books_url = "http://bookpickings.brainpickings.org/"
doc = Nokogiri::HTML(open(books_url))
puts 
books.each do |book|
   title = book.at_css(".post_title h1").text

   db.execute("INSERT INTO books (title) 
                 VALUES (?)", title)
end
{% endcodeblock %}

Fantastic. This works. Database is populated.


### Rails C in Rails Environment ###

Consider these two methods:

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}
def cached_repos
  cache[:repos]
end

def repos_not_on_gitbo
  cache[:repos].select do |repo_name|
    true unless Repo.find_by_owner_name_and_name(self.nickname, repo_name)
  end
end
{% endcodeblock %}

One will show you all of the repos available, the other will only show repos that do not already belong to the user. How can I make sure that this method works correctly? Fire `rails c` in your **active application folder** and test it.

{% codeblock [brainpickings-scraper.rb] [lang: Ruby] %}
[17:26:28] (master) gitbo
$ rails c
 Loading development environment (Rails 3.2.8)
001:0 >  #check all available attributes for Repo
?>                                    Repo.first
  SCHEMA (6.8ms)  PRAGMA table_info("repos")
  SCHEMA (0.2ms)   SELECT name FROM sqlite_master WHERE type = 'table' AND NOT name = 'sqlite_sequence' AND name = "repos"
  SCHEMA (0.2ms)  PRAGMA table_info("repos")
  Repo Load (0.2ms)  SELECT "repos".* FROM "repos" LIMIT 1
  Repo Load (0.2ms)  SELECT "repos".* FROM "repos" LIMIT 1
=> #<Repo id: 17, name: "omniauth", owner_name: "intridea", description: nil, watchers: 3450, open_issues: 26, created_at: "2012-11-16 21:45:21", updated_at: "2012-11-19 16:04:48", slug: "omniauth", git_updated_at: "2012-11-19 13:37:13">
003:0 > #test method
?>                                    Repo.find_by_owner_name_and_name("innatewonderer", "Test-Repo-for-Gitbo")
  Repo Load (0.3ms)  SELECT "repos".* FROM "repos" WHERE "repos"."owner_name" = 'innatewonderer' AND "repos"."name" = 'Test-Repo-for-Gitbo' LIMIT 1
  Repo Load (0.3ms)  SELECT "repos".* FROM "repos" WHERE "repos"."owner_name" = 'innatewonderer' AND "repos"."name" = 'Test-Repo-for-Gitbo' LIMIT 1
=> #<Repo id: 22, name: "Test-Repo-for-Gitbo", owner_name: "innatewonderer", description: nil, watchers: 0, open_issues: 2, created_at: "2012-11-16 21:52:15", updated_at: "2012-11-18 16:16:16", slug: "test-repo-for-gitbo", git_updated_at: "2012-11-16 16:10:46">
005:0 > #SUCCESS
{% endcodeblock %}

### 'Inspect Element' in Chrome ###

Chrome offers several nifty features that make developer's life easier. Right-click on the element => 'Inspect Element' or Command+Shift+c will bring up Developer Tools window on the bottom of the screen. [`Console Tab`](https://developers.google.com/chrome-developer-tools/docs/console) can be used to inspect the DOM, debug JavaScript or analyze HTML parse errors.

Remember the example I displayed at the beginning of this post in my Nokogiri project?

{% img /images/bookpickings.jpg %}

Looks familiar?

Be smart and seek out helper tools to do your work efficiently.  
Test lines your don't understand.  
Test methods you just created.  
PLEASE, Work off a separate branch.  
Test your commits.  
Enjoy it :)  
