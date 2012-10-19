---
layout: post
title: "Variable Scope"
date: 2012-10-18 20:02
comments: true
published: true
categories: 
---

Variable is an essential building block of any programming language. It is a way to store information and assign a name to it for future use. Variables come in all shapes and sizes. Anything from an integer to a string of characters can be used to reference data in the program.

###There are four main types of variables:

{% img right http://public.arnau-sanchez.com/ruby-functional/pics/functional-programming-joke.png 350 190 %}

* $global_variable
* @@class_variable
* @instance_variable
* local_variable (use [a..z] or _ )
  
Ruby comes with two pseudo-variables _nil_ and _self_ that do not accept values. _Nil_ is assigned to uninitialized variables. _Self_ will always refer to the object currently being executed. 

Looks simple, right? It gets somewhat confusing when you try to define the scope of each variable. Even more confusing, when you try to call on a variable that is does not belong to your current scope.

Ruby is always here to help you. **defined? variable** will show you the what the scope of selected variable. 

{% codeblock lang:ruby %}
	@@var = "class variable"
	
$ irb
001:0 > defined? @@var
{% endcodeblock %}

{% codeblock lang:ruby %}
 class Code
	var = "class variable"
 end

$ irb
001:0 > defined? var
{% endcodeblock %}

#### Debugging

If you run this code, it will give Object(NameError), which means that the variable you are trying to call on is currently out of scope. To solve this error locate where you first introduced the variable and either change its scope or rename the second variable. 

##Local Variable

**local_variable** can be declaired and referenced only within given scope (method, loop, etc). 

##Instance Variable

**@instance_variables** only belong to the given instance of an object. In an example below, when @instance_variable is changed in some_method, it retains its value when called in some_other_method. 

{% codeblock lang:ruby %}
class CodeBlock
	@instance_variable = "string"
	
	def some_method
		@instane_variable = 15 <== 15
	end

	def some_pther_method
		@instane_variable <== 10
	end
end
{% endcodeblock %}

##Global Variables

**$global_variables** are set to access anywhere in the program. It is ruby's convention NOT to use global variables. 

{% blockquote @aviflombaum https://twitter.com/aviflombaum %}
“... global variables? 
They pollute the planet. 
You know who uses global variables? 
PHP”
 {% endblockquote %}

Debugging will become a nightmare, if you redefine a global variable somewhere in your program, and then try to call on its original value.
Ruby offers us a number of major system variables. Aliases will come handy when working on bigger applications. 

|  **Symbol**      |           **Description** 			   	|
|:--------------:| :------------------------------------------:|
| $!	         | latest error message
| $@	         | location of error
| $_	         | string last read by gets
| $.	         | line number last read by interpreter
| $&	         | string last matched by regexp
| $~	         | the last regexp match, as an array of subexpressions
| $n	         | the nth subexpression in the last match (same as $~[n])
| $=	         | case-insensitivity flag 
| $/	         | input record separator
| $\	         | output record separator
| $0	         | the name of the ruby script file
| $*	         | the command line arguments
| $$	         | interpreter's process ID
| $?	         | exit status of last executed child process

##Class Variables

A class variable are defined and availbale **only** inside that class, meaning that only **one variable value exists for all objects represented by that instance within that class**. @@variable will be available for reference in any methods that might be defined for that class.
{% codeblock lang:ruby %}
class Code
	@@class_variable

	def class_method
		@@class_variable.reverse
	end
end
{% endcodeblock %}

Variables are your friends. Learn them, love them.