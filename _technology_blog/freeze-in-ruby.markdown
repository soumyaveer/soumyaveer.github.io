---
layout: post
title: Freezing Objects in Ruby
date:  2018-09-14 16:00:00
categories: main
banner_image: "freezing-objects-in-ruby.gif"
---
In the last post we talked about Variables.
 
Variables can also be declared as a constant. **Constant** starts with uppercase letters, like so,  `PI = 3.14`. Declared inside the class their scope is within the class. Declared outside, they can be accessed globally.

But declaring a constant variable makes it immutable? No. It does not.

  ```
    VAR1 = 10
    > 10
    VAR1 = 20
    (irb):2: warning: already initialized constant VAR1
    (irb):1: warning: previous definition of VAR1 was here
    > 20
  ```
  
Trying to change a constant will throw a warning but it can still be mutated.

Do we have a way to make constants immutable?

Yes, we do! The answer is - **Freeze**.

Objects in Ruby can be frozen using `Object.freeze` method. **Freeze** creates constants that can't mutate.

  ```
    numbers = [1, 2, 3]
 
    numbers.frozen?
    > false
 
    numbers.freeze
 
    numbers << 4
    > RuntimeError: can't modify frozen Array
 
    numbers.frozen?
    > true
 
    numbers = [5, 6, 7] 
    > [5, 6, 7] #object_id chages. Now it is pointing to different object.
 ```