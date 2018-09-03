---
layout: post
title: Method Lookup in Ruby
date:  2018-08-30 23:00:00
categories: main
banner_image: "method-lookup.jpg"
---

Every object is Ruby is an instance of class `BasicObject`. We can say that class `Object` is the parent of all the classes and class `BasicObject` is the parent of `Object`. And that is the way method lookup is Ruby works. But, the method lookup has more elements to it. Mixing of modules complicates the matter a bit. 

When the method is invoked, receiver checks its class for the method. If it finds the method it executes it. If not, it looks for it in any module that was
included. If the method is not found in that as well, it traverses up to the parent of the class which is `Object` and looks for the method. If it finds the method, its executed, if not, it traverses up to its parent class which is `BasicObject`. If the method is not present in `BasicObject` as well, it executes `method_missing`.

In the example below, we have class `User`, whose parent is class `Object` and has a module `Naming` included to it. `Object` has a parent `BasicObject` and includes an inbuilt module `Kernel`.

```ruby
  class BasicObject                 # Parent class of Object
    def method_missing(*args)
      raise "method not found"
    end
  end
  
  module Kernel                     # Mixed in Kernel module
  end
       
  class Object < BasicObject        # Parent class of User
    include Kernel
    def method_missing(*args)
      super
     end
  end
       
  module Naming                    # Mixed in Naming module
  end
       
  class User < Object              # Class User created by us           
    include Naming
  end
       
  user = User.new
  user.say_hello                   # Looking for method say_hello
   
```

Diagrammatic representation of method lookup in case of our example.

 ```
 class BasicObject (Method lookup ends at this point. Finally reaching BasicObject class. Does not find say_hello here also and executes method method_missing.)
       /\
       | 
 module Kernel     (Tries to locate say_hello in module Kernel. Does not find it.)
       /\
       |
 class Object      (Moves on to the parent class of the User, and tries to locate say_hello. Does not find it.)
       /\
       |
 module Naming     (Proceeds to find say_hello in module Naming. Does not find it.)
       /\
       |
 class User        (Tries to find say_hello in class User, but does not find it.)
       /\
       |
 user.say_hello    (Lookup starts from this point. Method say_hello is invoked)
 
 ```