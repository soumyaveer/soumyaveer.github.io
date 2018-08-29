---
layout: post
title: Method Lookup in Ruby
date:  2018-08-29 23:00:00
categories: main
banner_image: "coding.jpg"
---

Every object is Ruby is an instance of class `BasicObject`. We can say that class `Object` is the parent of all the classes and class `Basic Object` is the parent of `Object`. And hence that is the way method lookup is Ruby works. But, the method lookup has more elements to it. Mixin of modules complicates the matter a bit. 


When the method is invoked, receiver checks its class for the method. If it finds the method it executes it. If not, it looks for it in any module that was
included.If the method is not found in that as well, it traverses up to the parent of the class which is `Object` and looks for the method. If it finds the method, its executed, if not, it traverses up to its parent class which is `Basic Object`. If the method is not present in `Basic Object` as well, it executes `method_missing` function.

In the example below, we have class `User`, whose parent is cl;ass `Object` and has a module `Naming` included to it. And `Object` has a parent `BasicObject`. `Object` also has an inbuilt module `Kernel`.

```ruby
  class BasicObject                # Parent class of Object
    def method_missing(*args)
      raise "method not found"
    end
  end
  
  module Kernel
  
  end
       
  class Object < BasicObject       # Parent class of User
    include Kernel
    def method_missing(*args)
      super
     end
  end
       
  module Naming                  
  end
       
  class User < Object            
    include Naming
  end
       
  user = User.new
  user.say_hello
   
```

The method lookup in  this case will go like this:

 ```
        Class BasicObject (Finally reaches BasicObject class. Does not find say_hello here also and executes method method_missing.)
              /\
              | 
        module Kernel     (Tries to locate say_hello in module Kernel. Does not find it.)
              /\
              |
        Class Object      (Moves on to the parent class of the User, and tries to locate say_hello. Does not find it.)
              /\
              |
        module Naming     (Proceeds to find say_hello in module Naming. Does not find it.)
              /\
              |
        Class User        (Tries to find say_hello in class User, but does not find it.)
              /\
              |
        user.say_hello    (Method say_hello is invoked)
 
 ```