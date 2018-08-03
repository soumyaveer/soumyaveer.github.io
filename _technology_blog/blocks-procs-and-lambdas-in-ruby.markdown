---
layout: post
title: Blocks, Procs and Lambdas in Ruby
date:  2018-08-03 16:00:00
categories: main
banner_image: "blocks_procs_lambdas.jpg"
---
What are **Blocks** , **Procs** and **Lambdas** ? 
They are a group of statements that can be executed. They all might look similar and they are the extension of same concept `callable objects` in Ruby, but they have subtle differences.

* __Blocks__: 
    
    * A block is a way of grouping statements. They may appear only in the source adjacent to the method calls. 
    * They are a piece of code that accepts arguments, and returns a value and are always passed to a method call. 
    * Ruby's standard is to use braces for the single line blocks `{}` and `do end` for the multiline blocks.
     
      Example:
     
    ```ruby
    
     # Single line block
     [1,2,3].each { |x| puts x*2 }
   
		
	 #multi line block
      [1,2,3].each do |x|
        puts x*2  # block is everything between the do and end
     	end
      
	```
 
* __Procs__: 
     
    * `Proc` objects are block of code that have been bound to a set of local variables. Once bound the code might be called in different contexts and still access those variables.
       
   ```ruby
    toast = Proc.new do
      puts 'Hello World!'
     end
          
    toast.call #=> returns "Hello World!"
   ```
      
  Together `blocks` and `procs`, is the ability to take a block of code (code in between do and end), wrap it up in an object (called a _proc_), store it in a variable or pass it to a method, and run the code in the block whenever you feel like (more than once, if you want). 
  We use `procs` when we want to wrap a block in object and pass it around.
    
  The table below might make the difference between `blocks` and `procs` clearer.
  
   |SN | *Procs*                                    | *Blocks*                                            |
   |---| ------------------------------------------ | -------------------------------------------------   |
   |1. |  Procs are objects                         |  Blocks are not objects                             |
   |2. |  You can pass multiple Procs in a method   |  Atmost one block can appear in an argument list    |
  
  <br/>
  
* __Lambda__:
  
  * Similar to `proc`, `lambda` returns the a `Proc` object, using the provided code block.
 
    Though `proc` and `lambda` both return an object, they are different. The table below might make them a bit clearer.
  
  |Sn.|    *Procs*                                                                       | *Lambda*                                                        |
  |---| -------------------------------------------------------------                    | -------------------------------------------------------------   |
  |1. |  Procs do not check the number of arguments being passed to it.                  |  Checks number of arguments being passed to it.                 |
  |   |  When no arguments are passed, it assigns nil value to variables                 |  If arguments are required and not passed, it raises exception  |
  |2. |  When `return` is called in Proc, it exits the method it is called in            |  When `return` is called inside lambda, it exits the lambda code|
  |3. |  No explicit creation required. Using a `call` on block, creates a `proc` object | Needs to be created explicitly                                  |
   
   <br/>
      
  ```ruby
        
    lam = lambda { |x| puts x }    # creates a lambda that takes 1 argument
    lam.call(2)                    # prints out 2
    lam.call                       # ArgumentError: wrong number of arguments (0 for 1)
    lam.call(1,2,3)                # ArgumentError: wrong number of arguments (3 for 1)
         
    proc = Proc.new { |x| puts x } # creates a proc that takes 1 argument
    proc.call(2)                   # prints out 2
    proc.call                      # returns nil
    proc.call(1,2,3)               # prints out 1 and forgets about the extra arguments
      
   ```