---
layout: post
title: Variables in Ruby
date:  2018-09-07 16:00:00
categories: main
banner_image: "variables-in-ruby.jpeg"
---

__Variables__ are the places in memory locations that hold data. Every programming language provides variables including Ruby.

Ruby has four types of variables:
  
   1. __Global Variables__: A global variable has a name beginning with `$`. It can be referred to from anywhere in a program. Before initialization, a global variable has the special value `nil`.
    
      ```ruby
      $FILE_PATH = "/store/albums/songs" #global variable. Scope - complete program. 

      class Album
      end
      ```
   
   2. __Local Variables__: Local variables begin with a lowercase letter or an underscore. The scope of a local variable is confined to the code construct within which it is declared.
   
      ```ruby
      
      class Album
        def song
          name = 'Shape of you'  # name is a local variable. Not accessible outside this method. It's scope is limited to only this method.
        end
      end
      
      ```
   
   3. __Class Variables__: Class variables begin with `@@` and are shared by all instances of the class that it is defined in. A class variable is accessible to the entire class––it has _class scope_. Class variables store information regarding the class as a whole.
   
        ```ruby
        
         class Album
           @@album_count = 0 #class variable. Accessible to entire class.
         end
         
        ```
        
        * Can class variables be accessed from class methods? 
        
          Yes, class variables can be accessed by class methods. 
          
          ```ruby
            class Album
              @@artist = "Ed Sheereen"
    
              def self.artist
                # Return the value of this variable
                @@artist
              end
            end
            
            p Album.artist #=> "Ed Sheereen
          ```
        
        * Can class variables be access from instance methods?
        
          Yes, class variables can be accessed from instance methods. 
           
          ```ruby
            class Album
              @@artist = "Ed Sheereen"
    
              def artist
                # Return the value of this variable
                @@artist
              end
            end
            
            album = Album.new
            p album.artist #=> "Ed Sheereen
          ```

   4. __Instance Variables__: An instance variable has a name beginning with `@`, and its scope is confined to whatever object `self` refers to. Two different objects, even if they belong to the same class, are allowed to have different values for their instance variables. From outside the object, instance variables cannot be altered or even observed (i.e., ruby's instance variables are never public) except by whatever methods are explicitly provided by the programmer. 
   
      ```ruby
       class Album
        def songs
          @name = 'Shape of you' #instance variable.
        end
        
        def to_s
          @name.capitalize  #accessible inside class
        end          
       end
           
      ```
      
      * Can instance variables be accessed from class methods?
      
        No, instance variables cannot be accessed from class methods.
        
        ```ruby
          class Album
            def artist
              @artist = "Ed Sheereen" 
            end
            
            def self.fav_artist
              @artist.upcase
            end

           end
            
          p Album.artist # => "Ed Sheereen"
          p Album.fav_artist #=> Error. upcase on undefined
        ```
      * Can instance variables be accessed from instance methods?
      
        Yes, instance variables can be accessed from instance methods.
        
        ```ruby
          class Album
            def artist
               @artist = "Ed Sheereen"
            end
                     
            def fav_artist
               @artist.upcase
            end
          end
            
          album = Album.new          
          p album.artist # => "Ed Sheereen"
          p album.fav_artist #=> "ED SHEEREEN"
        
        ```
