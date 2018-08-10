---
layout: post
title: Namespacing in Ruby
date:  2018-08-10 13:00:00
categories: main
banner_image: "namespacing.jpg"
---
 **Namespacing** is a way to group the objects that are logically related to each other, and **Modules** is the tool that is used to achieve this.
 
From the time I started learning Ruby, I learned about **Classes**. **Modules** are similar to classes in the sense that they both contain methods, constants, etc. They are even defined in a similar way. _Classes_ are defined with the keyword `class` where as to define _modules_, we use keyword `module`. 

Though classes and modules may look similar, they are not same. You cannot replace one with another, because classes can be instantiated where as modules cannot. I will not go into the details of their differences because this post is solely about modules and namespacing.
  
 If modules cannot be instantiated, Why use them at all?
  Because using modules are beneficial in a few ways.
  
1. __Modules prevent name clashes.__ : They create a kind of package in which the methods and constants can exist without being interfered or over-ridden by other methods and constants of the same name.
    
   ```ruby
         
         module Play
           class SnakesAndLadder
             def dice(number)
              puts "Playing Snakes and Ladder with #{number} dice/dices"
             end
           end
         end      
                  
         module Cook
           class MixedVegetable
              def dice(vegetable)
                puts "Cooking Mixed Vegeteable. Dicing #{vegetable}"
              end
            end
         end
         
         snakes_and_ladder = Play::SnakesAndLadder.new
         snakes_and_ladder.dice(1) 
         #=> "Playing Snakes and Ladder with 1 dice/dices"
         
         mixed_vegetable = Cook::MixedVegetable.new
         mixed_vegetable.dice("Onions") 
         #=> "Cooking Mixed Vegeteable. Dicing Onions"
 
   ```
                                                             
2. __Modules help with implementation of mixins__ : _Mixins_ gives us a way of adding functionality to the classes. Mixin is basically a module included to the class. When a Module is mixed in a class, the class will have access to the methods of the Module. In Ruby, _Multiple Inheritance_ is not allowed with classes. Modules also help us implement _Multiple Inheritance_.
    
   ```ruby
      class Song
        attr_accessor :name, :artist, :duration
        # include comparable class which gives us access to 
        # all the six comparator  methods (<, <=, ==, >, >= and between?)
 
        include Comparable
           
        def initialize(name, artist, duration)
          @name = name
          @artist = artist
          @duration = duration
        end
 
        # define spaceship operator.
        # As a class writer, you define the one method,
        #  <=>, include Comparable, and get six comparison functions for free.
         
        def <=>(other)   
          self.duration <=> other.duration
        end
      end       
          
      song1 = Song.new("Shape of You", "Ed Shereen", 225)
      song2 = Song.new("Cheap Thrills", "Sia", 300)
      song1 <=> song2	#=>	-1
      song1  <  song2	#=>	true
      song1 ==  song1	#=>	true
      song1  >  song2	#=> false
    ```
