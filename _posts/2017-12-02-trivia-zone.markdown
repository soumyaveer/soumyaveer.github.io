---
layout: post
title: TriviaZone - A fun way of testing your knowledge on the topics you love!
date:  2017-12-02 13:25:00
categories: main
banner_image: "bookshelf.jpg"
summary: Play or create trivia of the topics you love and compete for your name on the leaderboard.
---

The most difficult part before starting any project is to come up with something really interesting to work on. During my research for this project, I realized that my last two projects were confined to _Books_, and I wanted to expand further on this. I wanted to create something for everyone - lovers of painting, movies, books and programming like myself, etc. This is how I came up with the idea of creating **TriviaZone**, an application which is a combination of fun as well as learning experience.

What is **TriviaZone**? As the name suggests, this is an application that allows you to play or create your favourite trivia and compete for the top three positions on the Leaderboard.

**From user's point of view**, this application provides user with multiple features:
1. User can _sign_up_ for an account or _sign_in_ in case the account is already present.
2. User can also _sign_up_ or _sign_in_ via _Facebook_.
3. Once, signed in, User can see the scores of his or her previously played trivias.
4. User is provided with options to _Add a new Trivia_, _Play Trivia_, _Search a Trivia_ or check the _Leaderboard_.
5. The options of _editing_ or _deleting_ the trivia created by him/her are also provided . (User is not authorized to _edit_ or _delete_ trivia created by any other user.

**From technical point of view**, **TriviaZone** is created on _Ruby on Rails_ framework. The main challenges that I came across while working on this project were:
1. Two levels of `form nesting`.
2. The integration of gems `devise` and `omniauth`.
3. Multiple routes needed `nesting`.
4. Handling of `unpermitted strong parameters`.
5. Thinking of a way to capture the correct answers after the trivias were played.

After spending a lot of days debugging, reading and re-reading tutorials, I successfully overcame these challenges. Every hour spent was a great learning experience which left me with a little more knowledge than I had when I stared with this project. I am over joyed with the fact that I decided to work on **TriviaZone**.
