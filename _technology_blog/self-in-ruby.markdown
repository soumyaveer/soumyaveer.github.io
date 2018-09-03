---
layout: post
title: Ruby's Self
date:  2018-08-19 23:00:00
categories: main
banner_image: "self.gif"
---

Ruby being an Object-Oriented language has the concept of `self`, but what is `self`?
If you said, "It means current object". You are right. But it is a bit more complicated than that.
The keyword `self` in ruby gives access to the current object - the object that is receiving the current message. A method call in ruby is actually a message being sent to the receiver. When we write `object.say_hello` , we are sending the message say hello to the receiver `object`. `object` will respond to `say_hello` if there is a method body defined for it. 
   
Inside the class `self` would mean the class itself, outside class `self` means `main`.
   
   ```ruby
    class Person
      def i_am
        self    
      end
      
      def self.i_am
       self
      end
    end
 
    person = Person.new
    person.i_am  #=> #<Person:0x007fba740dc790>
    Person.i_am #=> Person
    self #=> main
   ```