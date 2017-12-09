---
layout: post
title: ...and these were the lessons I learnt from previous projects.
date:  2017-12-08 13:25:00
categories: main
banner_image: "mistake.jpg"
summary: While working on projects, I made many mistakes and learnt from them. Here is a blog discussing my mistakes and takeaways.
---

> “Experience is what you get when you didn't get what you wanted. And experience is often the most valuable thing you have to offer.” ― Randy Pausch, The Last Lecture

Successful completion of a project is not enough, it is also important to learn from your mistakes. Also, I think it is more important to share your mistakes with everyone, along with your success story. So, here are some mistakes I made and lessons I learnt from them :

  1. **Pen down your ideas on paper before starting a project** :
     On numerous occasions we have heard programmers say "Think before you code". And it is absolutely true. Coding without thinking is the biggest mistake one can make. Trust me, it can get you all jumbled up. Whenever you think that you have a great idea, go ahead and do some _back of a napkin_ design. Write down the flow diagram, draw the models and design your website on paper. Make sure you know the flow and understand the models completely.

  2. **Write tests before you start writing the code** :
      Yes, that's a very common mistake. I still haven't completely overcome the urge to start writing the code before tests. But, it does land me in trouble every time I do it. _Test Driven Development(TDD)_ is a very important practice.

      First, when you write tests, you are describing the behaviour of your code. You are writing down what is to be expected from your piece of code, what should be the input and what will be the return value. While doing this, you understand your code better and what you expect the result to be.

      Second, once you write a piece of code, the test will help you debug the code faster. You can keep making the changes and running the tests till it returns the expected value. I think it is better to resolve errors in this way, rather than refreshing the webpage and checking if the error is fixed.

      Third, with tests you can catch the boundary condition exceptions which might get overlooked if you are testing your website by refreshing it.

  3. **Format your code from the beginning** :
    Formatting is important for the readability, not only for others but for the one who is coding as well. Imagine revisiting a piece of code after six months and finding that you don't understand anything that you wrote. I won't even mention someone else trying to review your code. You might think, "Oh! I'll format it later". When you start formatting in the final phases, you'll realize what a waste of time it is. Yes, you can use _indent all_ on every file, but some times _indent all_, doesn't indent properly. So, I think formatting while you are working on a file is better than revisiting it later.

  4. **Follow the best code style practices from the beginning** :
    "Let me get this code working, code style is secondary". Yes! I have been there and trust me that's the worst thing I did to myself. When I executed `rubocop` and `scss-lint` style checks, I literally fell out of my chair and stared at the message `300 errors and 50 warnings found!` (it wasn't even a big project!). It took me more than two hours to fix them all. Please, don't do this to yourself. Adhere to the code style practice from the beginning.

  5. **Update your seed data along your models**:
    _Seeding data_ is very important, it helps you add data to database quickly. All one has to do is run the seed file instead of writing create sql in console everytime. For example, if you need to fill 10 tables with data, instead of writing 10 create SQL's , you can just run one seed file. But, if you update your model and forget all about updating your `seed` file, it will be a total waste of time revisiting it later.

      First, the purpose of seed file is defeated. If you are updating the seed data later means you ended up manually adding data to the database.

      Second, you'll have to revisit the models and update it later, which feels like a waste of time after you have finished your project.

 6. **Try to keep you code DRY(Don't Repeat Yourself)** :
    In some scenarios, you write the code and later realize that the code needs to be DRY. In those cases, it's fine to extract the code to a method or partial later. But in some cases, like `new` and `edit` forms, where you know that the form will be identical, it is better to extract and reuse it rather than writing the whole piece of code multiple times and than extracting it to a partial. It is a nightmare to revisit the whole code in search of repeated content.

 7. **When you come across a complicated problem, try to break it down** :
 Multiple nested params? A huge piece of complicated code? Time to break it down into smaller pieces!
 Don't waste your time trying to handle a huge complicated code all together. Handling complicated pieces of code like multiple nested params sometimes looks like a daunting task, but it becomes easier once you break it down and try to understand the smaller pieces of it.

 8. **Write comments wherever necessary** :
  I realised the importance of comments during my last project. While working on that project I had to take a break of around a month. When I returned and opened the Editor, I realised that I have totally lost track of what I was doing before I left. It took me few hours of digging my notes, finding my models and website design and reading and re-reading them to get back on track. If only I had left comments in the files, I would have saved a few hours!

 9. **Commit your code every few minutes** :
 I'll tell you a story here. It begins, when I new to Ruby and Github. At that time I was in a habit of saving data on my local desktop and  committing it once or twice in two days. One day while I was working on my laptop, it crashed. I had to reformat the laptop to fix it. With that crash I lost two days of hard work. Moral of the story: Keep committing and pushing the data. It's very frustrating to do the same work over and over again.

    Not only that, Committing is also important because it records what changes you made in your work. It's a history of your work. The more accurate it is, the better. And the best way to make it accurate is to commit every few minutes.

These are some of the major mistakes I made while working on the projects. I learnt a lot from them, sometimes the hard way. Hope someone else will also be able to learn something from my mistakes.
