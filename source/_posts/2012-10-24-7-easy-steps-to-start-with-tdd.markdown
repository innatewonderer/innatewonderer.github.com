---
layout: post
title: "7 easy steps to start with TDD"
date: 2012-10-24 18:26
comments: true
categories: 
published: true 
---

1:00 pm - TDD is a very useful tool in software development...

3:30 pm - Test driven development or TDD can be extremely frustrating, time consuming and sole devouring experience. 

6:00 pm - Be patient. Like a sorority club, TDD will put you through a tidious initiation ceremony. Once, accepted, you will be able to produce a much cleaner code and improve your style. 

Few easy steps to get you started with TDD using **[rspec](https://rubygems.org/gems/rspec)**.

Tools used:

* Sublime Text 2
* Terminal
* gem of choise: rspec
* original assignment: by [Avi Flombaum](http://twitter.com/aviflombaum) can be found in my [GitHub repo](https://github.com/innatewonderer/playlister-jenya).

### Step 1 : Installing rspec 

Create a new folder for your project, cd to that folder and run **gem install rspec**. 

{% img /images/rspec_tdd-Jenya@Flatiron-Air-1-bash-122×30.jpg %}

	**TIP**
	**spec_helper.rb** will hold all of the required paths for you.
	Do not forget to include all necessary files, gem names, and libraries.
	_require 'spec_helper'_ will be the only line needed in your testing files.

{% codeblock spec_helper.rb lang:ruby %}

require 'rspec'
	require_relative '../artist'
	require_relative '../artist'
	require_relative '../song'
	require_relative '../genre'
require 'yaml'
{% endcodeblock%}

{% codeblock artist.rb lang:ruby %}
require 'spec_helper'
{% endcodeblock%}

### Step 2 : Identify what needs to be accomplished

I had a sample of tests completed for Ruby assignment using _assert_method_. By running this test, I can test if my program is able to create an instance of _artist_.

{% codeblock [assert_test] [ruby] %}
test 'Can initialize an Artist' do
	assert Artist.new
end
{% endcodeblock%}

### Step 3 : Write your test

{% img /images/artist_spec.rb-final_ruby_tdd.jpg %}

In artist_spec.rb, I need to be able to test that 

 - by calling _#new_ method on class variable **@artist** 
 - I will be able to create a new instance of artist 
 - that should be_an_instance_of Artist class. 

 (_What? Yes! It is all one sentence. 
 You don't like my overly explicit coding syntax? Sorry, get over it._)

	**TIP**

Stay on a safe side. Commit your code to a GitHub repository. Here is a great post on [how to get started with Git](http://cjbrock.github.com/blog/2012/10/23/5-easy-guides-to-help-you-get-started-with-github/).

### Step 4 : Run your test - FAIL 

{% codeblock %}
rspect artist_spec.rb
{% endcodeblock %}

Terminal will tell you exactly what is wrong with your test.

{% img /images/spec_jenya@Flatiron-Air-1_bash_107×13.jpg %}

### Step 5 : Fix your code

To pass this test we need to initiate class Artist.

{% codeblock [artist.rb] [ruby] %}
class Artist

end
{% endcodeblock%}

### Step 6 : Run your test again - PASS

{% img /images/Arc.jpg %}

### Step 7 : Do a happy dance  
{% img /images/original_art.jpg %}  
Original Work  

####Here is an example of a more complex test:
  
Create the test  
Test and Fail  
Fix your code  

{% img /images/Skitch-1.jpg %}

  Test and Pass

{% img /images/spec-jenya@Flatiron-Air-1-bash-164×8.jpg %}

  Happy dance anyone???  

{% img /images/original_art.jpg %}  


  **NOTE**  
  I plan to transofrm all test cases from original state to rspect. Feel free to [fork it here](https://github.com/innatewonderer/final_ruby_tdd).

 


