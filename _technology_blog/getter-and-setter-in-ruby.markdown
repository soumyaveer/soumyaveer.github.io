---
layout: post
title: Creating getter and setter in Ruby
date:  2018-09-21 21:00:00
categories: main
banner_image: "creating-getter-and-setter-in-ruby.jpg"
---

In Ruby, objects can't exist in isolation. They have to communicate with the other objects. *Instance variables* ([Variables is Ruby](https://www.soumyathinks.com/technology/blog/variables-in-ruby)) can be accessed only by object's own methods. Therefore, we use **getter**, which is responsible for returning the value of an instance variable and a **setter** which is responsible for setting the values of instance variables.

getter and setter methods can be created in 2 ways:
   
1. `attr_*`: 
  * `attr_reader`: generates getter method.
  * `attr_writer`: generates setter method. 
  * `attr_accessor`: generates getter and setter methods.
  
2. Manually: We can manually create getter and setter methods. If we write a method say, `ticket`, this will be a getter and `ticket=` will be setter method.
   
```ruby
    class Person
      attr_reader :name               # creates getter method for name
      attr_writer :address            # creates setter method for address
      attr_accessor :phone_number     # creates getter and setter methods for phone number
     
      def name=(name)                 # manually creating setter
        @name = name
      end
     
      def address                     # manually creating getter
        @address
      end
    end
 ```