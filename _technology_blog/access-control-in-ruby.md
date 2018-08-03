---
layout: post
title: Access Control in Ruby
date:  2018-07-27 16:00:00
categories: main
banner_image: "Control3.jpg"
---
Ruby is an object-oriented language, which means that every object is an instance of a class and every object has certain behaviors (methods). Access control is a way in which Ruby protects the behaviors (methods) defined in a class.

Ruby provides three levels of access control:

  1. __public__ : Public methods can be called by everyone - no access control is enforced. A class's instance methods are public by default, which means anyone can call them.

  2. __private__ : Private methods cannot be called with an explicit receiver - the receiver is always `self`. Private methods can be called only in the context of current object, you cannot invoke another objects private method. To make methods private, we use `private` keyword before writing a method.

  3. __protected__: Protected methods are like __private__ methods. These methods can be invoked only by objects of the defining class and its subclasses. Access is kept within the family. `protected` has limited usage. To make methods protected, we use `protected` keyword before writing a method.
  
  In the example below, we have  class `Album` and a Subclass - `CD`
  
   ```
     class Album
       def song
         @name = 'Shape of you' # public method
       end
          
       # in method title I am accessing protected method - self.artist and private method - genre.  
       # Note: if I say self.genre in place of genre, ruby will throw an error. Reason? You cannot call private methods on explicit reciever
        
       def title
         "#{self.artist} - #{genre}"  
       end
          
       protected

       def artist
         @artist = 'Ed Shereen' #protected method
       end

       private

       def genre
         @genre = 'Pop' #private method
       end
     end
        
     album = Album.new
     => #<Album:0x007f8a6482bb58> 
        
     album.song
     => "Shape of you"  #=> accessing public method of class Album
        
     album.title
     => "Ed Shereen - Pop" #=> public method of class Album
        
     album.artist  #=> protected method of class Album
     NoMethodError: protected method `artist' called for #<Album:0x007f8a6482bb58 @name="Shape of you">
        
     album.genre  #=> private method of class Album
     NoMethodError: private method `genre' called for #<Album:0x007f8a6482bb58 @name="Shape of you">
        
     # creating a class CD which is a subclass of Album
        
     class CD < Album
        
       def name_sticker   
         self.artist         # name_sticker access the protected method of Album class
       end
     end
        
     cd = CD.new
     => #<CD:0x007f8a64143778>
     
     cd.name_sticker        # public method of class CD
     => "Ed Shereen"
      
     cd.title               # public method of class Album which accesses private method of Album class
     => "Ed Shereen - Pop"
      
     cd.song                # public method of class Album
     => "Shape of you"
      
     cd.artist              # protected method of class Album. It should be noted that you cannot access method artist from outside the class, but you can access it inside the subclass
     =>NoMethodError: protected method `artist' called for #<CD:0x007fa0fd9c0810>
      
     cd.genre               # private method of class Album.
     =>NoMethodError: private method `genre' called for #<CD:0x007fa0fd9c0810>
        
   ```

 
 The table below might make the differences between the three access controls - `public`, `protected` and `private`  a bit clearer:

 | Methods    | Inside Class                                | Outside Class                | Inside Sub-Class              |
 | ---------- | ------------------------------------------- | ---------------------------- | ----------------------------- |
 | Public     | Yes (public_method_name)                    | Yes (obj.public_method_name) |  Yes (public_method_name)     |
 | Protected  | Yes (self.protected_public_name)            | No                           |  Yes (protected_method_name)  |
 | Private    | Yes (But, Can't say self.private_method_name| No                           |  No                           |
