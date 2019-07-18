---
layout: post
title: 10 Things I learned from Clean Code
date:  2019-07-17 13:00:00
categories: main
banner_image: "clean_code.jpg"
---
Recently I finished reading **Clean Code** by -  _Robert C. Martin_ . This book taught me how to write good code, the pitfalls and things to look out for while writing code. Here are 10 things that I learned from **Clean Code**:

1. **Write code that can be understood by others** - 
    Writing a working piece of code is not enough. When you write code, keep in mind that it has to be read and understood by others. And not only them, at times it will have to be read and understood by you! Coming back to a piece of code and not understanding it is an unpleasant experience. Coming back to a piece of code and realizing that it was written by none other than you is even more unpleasant.

2. **Name your variables/methods/classes based on their responsibility** - 
	It is important to have good names for your variables, classes and methods. Half the battle of clean code is won if your naming is proper. Having good names ensures that there is no confusion in the responsibility of variables/methods/classes. If people won't understand what the responsibility of a piece of code is, they will add whatever they want resulting in messy, hard to understand code. 
	
	Having proper names reduces misdirection in understanding as well. For example, if your method is stripping numbers from keys, don't name it `increment_attributes`. This name not only fails to properly define the responsibility of the method, it actually gives wrong information.

3. **Use domain specific names** - 
	Try to base the names of your variables, methods , classes etc on the domain you are working on. For example, if you are working in mortgage industry, it is best to use names like `loan_application`, `borrower` or `home_equity`. These days there is a continuous flow of people in and out of the companies. Following this approach will ensure that if you are not sure what a piece of code is doing or why it is there in the first place, you can ask a domain expert. Because the naming convention is based on domain, a domain expert will be able to help you understand the requirements and the process.
	
4. **Commented out code is a dead weight** - 
   No code base should have commented out code. Commented code confuses developers - "why is this piece of code here, if it is not required?", "Has someone deliberately left it there?", "Is someone testing it?". Other developers don't know what to do with it. This creates clutter and results in bad rotting code. If you come across such code, feel free to delete it out. Make use of version control for future reference.

5. **Keep your methods and classes small** - 
	If you have too many lines in your method or class, chances are that they are performing too many responsibilities, hence breaking the *Single Responsibility Principle*. 
	
6. **Write tests for every feature** -
	Testing not only works as a safety net for the current feature that you might be developing, it also guards the pre built features by making sure that your new changes are compatible with your old code. It gives you confidence to write your code without breaking anything. Your tests should be as tight as possible. It might take a little longer to finish the work, but it will pay off in the long run.

7. **Your tests should be as well maintained as your code** - 
	It is easy to allow the tests to fall out of shape. You added a feature but did not write the test for it, or worse did not update the tests to accommodate testing of the extended feature. If your tests fall out of date, there is a high possibility that something major will fail and it won't be caught until the damage is already done.
	
8. **Don't use a comment when you can use a function or a variable** - 
   	Writing comments when necessary is a good practice. Complex pieces of code that are difficult to understand should have comments. But too many comments create noise. You do not need to write a comment for creating a new variable. Reading the code should be enough to explain that a new variable was created here. Avoid writing comments that create noise or are misleading. If a piece of code is changed, make sure to update the comments as well.
   
9. **A team of developers should agree upon a single formatting style** - 
   	Software should have consistent style. The conventions and code style should be decided upon by the team and followed by everyone. Different formatting styles add complexity to the code which is undesirable.
  
   
10. **Keep cleaning your code continuously** -
   It is easy to fall into the habit of cleaning up bad code. It is a doable but expensive endeavour. Sometimes, if the project is too big, you might not even get a chance to come back and clean your code. Writing a piece of code in morning and cleaning it in afternoon can be done. But it is difficult to write a piece of code today and clean it next year.
   
These are few things that I learned from reading the book. There is so much more in the books that remain unexplored in this blog. I highly recommend [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship-ebook/dp/B001GSTOAM/ref=sr_1_2?keywords=clean+code&qid=1563427667&s=gateway&sr=8-2) to all  developers who enjoy writing beautiful and clean code!
   
 
   
