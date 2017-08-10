---
layout: post
title: BookDeals - A CLI Data Gem
date:  2017-08-09 13:25:00
categories: main
banner_image: "bookshelf.jpg"
summary: Bookdeals is my second rubygem creation. This gem shows the book deals hosted on Goodreads website.
---

>"When I get a little money I buy books; and if any is left I buy food and clothes." - Desiderius Erasmus

There are many ways of gaining knowledge, but the one I like most is - **Reading a Book!** When I started this project, I wanted to create something that will be helpful in enhancing knowledge by reading. Being a passionate book lover, I decided that an application which gives the current available book deals will be an interesting project to work on. And this idea resulted in the creation of `gem book_deals`.

_What is `book_deals`?_  BookDeals is a gem which displays the latest book deals on Goodreads website.

The main focus while implementing `book_deals` was _creating a gem_ (The gem can be installed by following the `README` document provided with documentation.) and following _Object Oriented Programming_ principles.

From users point of view, it was important to look into the _ease of usability_ aspect. To conquer this, every step while executing `book_deals` was guided with helpful messages and color coded instructions.

Once, the user executes the program, he/she is greeted with a _Welcome screen_ followed by a _menu_. This menu contains a list of categories to select from.

```shell
Welcome to Book Deals!!
=======================

Select a Category to see the deals:

1. Today Only! (Press 1 to see Today Only!)

2. Bestsellers (Press 2 to see Bestsellers)

3. Romance (Press 3 to see Romance)

4. Mystery & Thrillers (Press 4 to see Mystery & Thrillers)

5. Fantasy & Science Fiction (Press 5 to see Fantasy & Science Fiction)

6. Fiction (Press 6 to see Fiction)

7. Nonfiction (Press 7 to see Nonfiction)

8. Young Adult (Press 8 to see Young Adult)

Enter your selection:

```

Now, if user wants to see the deals in category _Bestsellers_, he/she can press the number _2_ on the keyboard.
This displays the list of book deals with _book title_, _author name_, _description_, _deal price_, _original price_, _expiry date or time_ of the deal and the _deal purchase url_.

```shell
Enter your selection:
2

Deals for Category - Bestsellers

--------------------------------------

Book Title: Six of Crows (Six of Crows, #1)

Author:  Leigh Bardugo

Description: From the New York Times and USA Today-bestselling author of the Grisha Trilogy. Criminal prodigy Kaz Brekker has been offered wealth beyond his wildest dreams. But to claim it, he'll have to pull off a seemingly impossible heist and a crew desperate enough and dangerous enough to get the job done.

Deal Price: $2.99

Original Price: $9.99

Expires in: a month

This book can be purchased on: https://www.goodreads.com/book/show/22294935-six-of-crows?rto=x_gr_w_activedealspage_bp

==============================================================================

Book Title: Disclosure

Author:  Michael Crichton

Description: A New York Times bestseller. An up-and-coming executive at the computer firm DigiCom, Tom Sanders is a man whose corporate future is certain. But after a closed-door meeting with his new bossâa woman who is his former lover and has been promoted to the position he expected to haveâSanders finds himself caught in a nightmarish web of deceit in which he is branded the villain.

Deal Price: $1.99

Original Price: $5.99

Expires in: 3 days

This book can be purchased on: https://www.goodreads.com/book/show/35267827-disclosure?rto=x_gr_w_activedealspage_bp

==============================================================================
Total 12 deal/deals found for category Bestsellers.
==============================================================================
```

After displaying all the deals for the category, the user is prompted with the question "Do you wish to continue? (y/n)". If user selects _'y'_, than he/she can continue viewing deals. Otherwise, if user selects _'n'_, the program exits with a message, "Thank you for visiting BookDeals. Hope to see you soon. Goodbye!" .

```shell
Do you want to continue viewing deals? (y/n)

Enter your selection:
n

Thank you for visiting BookDeals. Hope to see you soon. Goodbye!
```
Working on this project was like a roller-coaster ride, filled with joy and excitement. It was also an unforgettable learning experience. Most enjoyable was the fact that I was creating something that I am passionate about - buying and reading books!

