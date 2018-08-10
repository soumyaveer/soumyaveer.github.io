---
layout: post
title: BookProgress - Track your reading progress
date:  2017-09-13 13:25:00
categories: main
banner_image: "book_progress.jpg"
summary: BookProgress helps you track your books, reading progress and see what others are reading.
---
> “A bookshelf is a biography written by others.” ― Kat Lehmann

Reading is my favourite hobby. Just like every book lover, I allot at least one hour to reading everyday. A few of months back I noticed a pattern - every night I sat and calculated what percentage of book I read that day. This triggered the idea of creating an app which will do the calculations for me and give me the percentage of how much I read. This is how _BookProgress_ was born.

**BookProgress** is an application which helps you keep track of your reading activities and the percentage of book completed.
Not only this, it also let's you see what other people are reading and their progress.

 The main focus while developing the app was on creating a user friendly GUI. In order to ensure that a user is authenticated and authorized to access and update only his/her account information, I created a _Signup_ page for the new users and a _Login_ page for the users who already had an account. Once, the user is logged in, he/she can add books and keep updating their progress or can delete a book from their shelf. User is allowed to see what his/her friends are reading, how many books and what is their progress, but he/she is not allowed to change the bookshelves of other _BookProgress_ members.

A _Sinatra_ based application, _BookProgress_ was created using the **Model-View-Controller** design pattern. It consists of three models `User`, `Book` and `BookProgression`. The database used was _SQLITE3_ and migrations were done using _ActiveRecord_. _Bootstrap_ was used to do styling of the website.

This project was not only a source of learning but also a source of joy. I enjoyed a lot working on the two things that I love most - Programming and Books!

Check out the source code of **BookProgress** [here](https://github.com/soumyaveer/book-progress).




