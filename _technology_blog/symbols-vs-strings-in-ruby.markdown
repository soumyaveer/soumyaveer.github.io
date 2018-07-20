---
layout: post
title: Symbols vs Strings in Ruby
date:  2018-07-20 13:00:00
categories: main
banner_image: "different_3.jpg"
---

`String` and `Symbol` are two built in ruby classes which give us ability of text manipulation. 

What are **Strings** ?
Anything inside the _quotations_ is a string. They are the instances of `String` class.

  ```ruby
   'Hi! I am a string in single quotations.' 
   "Hi! I am also a string but in double quotations."
  
  ```
  
 What are **Symbols** ?
 Symbols are instances of class `Symbol`. They can be identified by `:` in front of them.
 
   ```ruby
    :a_symbol
    :another_symbol
   ```



**Symbols** and **Strings** might be similar in a way that both of them can be used for manipulating text, but they have a lot of differences.

 1. **Symbols** are _immutable_. You cannot append another symbol to an existing symbol and create a new symbol.
  
    ```
     irb(main):171:0> :a << :b
     NoMethodError: undefined method `<<' for :a:Symbol
    ```
  
    **Strings** are _mutable_. You can append another string to an existing string and create a new string.
  
    ```
     irb(main):005:0> "a" << "b"
     => "ab"
    ```
   
     
 2. **Symbols** are _unique_. Same symbol will always represent the same object. Symbols are saved in `symbol_table`, every time we try to access a symbol, it retrieves it from the table, hence pointing to the same symbol.
        
        ```
          irb(main):041:0> var1 = :a
          => :a
          irb(main):042:0> var2 = :a
          => :a
          irb(main):043:0> var1.object_id
          => 723868
          irb(main):044:0> var2.object_id
          => 723868  # var1 and var2 are pointing to the same object
        ```
        
    **Strings** are _not unique_ . Same strings may represent different object. Creating two strings with same value may result is creation of a new instance of class `String` for each.
    
        ```
          irb(main):045:0> var3 = "a"
          => "a"
          irb(main):046:0> var4 = "a"
          => "a"
          irb(main):047:0> var3.object_id
          => 70276725479300
          irb(main):048:0> var4.object_id
          => 70276725462500  #var3 and var4 are pointing to different objects
        ```

    
 3. The presence of a **symbol** cannot be tested using `include?` method. As soon as you execute `include?`, it adds the symbol to the `symbol_table` and returns `true`. In order to test a symbol, we need to use `grep`.
        
        ```
          irb(main):050:0> Symbol.all_symbols.grep(/pqr/)
          => []
          irb(main):052:0> Symbol.all_symbols.include?(:pqr)
          => true
        ```
    
    **Strings** can be tested using `include?` method. 
    
        ```
          irb(main):006:0> "I am a string pqr".include?("pqr")
          => true
        ```

    
 4. As stated above, **Symbols** are saved in `symbol_table`. Every time a new symbol is created, it is stored in the table.
        
        ```
          irb(main):010:0> Symbol.all_symbols.count
          => 3488
          irb(main):011:0> :new_symbol
          => :new_symbol
          irb(main):012:0> Symbol.all_symbols.count
          => 3489 #=> count increased by 1
        ```
 
    **String** have no such table.
    
 5. Finally, Ruby can process **Symbols** faster because no new memory is allocated when they are referenced elsewhere.
    
    Ruby processes **strings** slower than symbols.

These are few important differences between Symbols and Strings.
