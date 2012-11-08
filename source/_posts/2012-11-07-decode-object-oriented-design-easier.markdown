---
layout: post
title: "Decode Object Oriented Design"
date: 2012-11-07 10:10
comments: true
categories: OOD, refactoring
published: true 
---

<!-- Instead of writing a post and then finding a good title, I am going to commit to finding at least five facts that will make OOD clear for me... As long as it takes :) -->

ODD has been around since mid 60's. The concept didn't really pick up untill early 90's with C++. It's receiving a lot of attention in Rails/Ruby community as well. The concept might appear hard to understand, but it's important. Below, I have attempted to collected resources and statements that suppose to make it clear to me.

<!-- more -->

###OOD includes: 

* Code that is broken down into separate objects that help to organize data
* Data isolated into restricted area where only specific procedured had access to it
* Objects that encourage reuse of code (minimal inner dependancies)
* Data that stays separate from actions
* Objects that represent one item

###[Object Oriented](http://www.tonymarston.net/php-mysql/what-is-oop.html) Language should include:

**Class**
  Blueprint/prototype that defined variables or methods common to all objects of a certain kind.

**Object**
  An instance of a class. A class must be instantiated into an object before it can be used in the software. More than one instance of the same class can be in existence at any one time.

**Encapsulation**
  Placing data and the operations that perform on that data in the same class. The class becomes a 'capsule' or container for the data and operations.

**Inheritance**
  The reuse of base classes (superclasses) to form derived classes (subclasses). Methods and properties defined in the superclass are automatically shared by any subclass.

**Polymorphism**
  Same interface, different implementation. The ability to substitute one class for another. This means that different classes may contain the same method names, but the result which is returned by each method will be different as the code behind each method (the implementation) is different in each class.


What ODD helps you do is to delegate most of the repetititve logical work *to the data itself*. Data is becoming active, instead of staying passive. 

### Lost yet?

Ask yourself the following questions. If you answer yes to any, refactor:

1. Is it the role of this class to know how to do something?
2. What should be defined as a class?
3. What sort of class hierarchy would be best?

### What's that smell? (simplified)

If you see any of the following in your code, refactor:

1. Duplication of code
2. Extensive length of class or method
3. Large amount of parameters


Resources:  
1. [Ruby User's Guide. Object-oriented thinking](https://speakerdeck.com/styliii/object-oriented-design)  
2. [Object Oriented Desing. Li Ouyang](https://speakerdeck.com/styliii/object-oriented-design)  
3. [Code Smells by Jeff Atwood](http://www.codinghorror.com/blog/2006/05/code-smells.html)  
