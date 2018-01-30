---
layout: post
title: TriviaZone - Making pages responsive
date:  2018-01-30 13:25:00
categories: main
banner_image: "trivia-zone.jpeg"
summary: In Trivia Zone we played and created new trivias, but doing the same is more fun when the pages are responsive.
---

**Trivia Zone** is an application that allows playing and creating trivias and compete for the top three positions on the Leaderboard. (Read more about **TriviaZone** [here](http://www.soumyathinks.com/main/2017/12/03/trivia-zone-a-fun-way-of-testing-your-knowledge.html)).
It was fun developing TriviaZone, but my end goals for working on these projects are - learning and improving the user experience. So I enhanced the application to implement what I learned in _Javascript_ & _Jquery_ and hence, improve the overall experience of the end user.

From user's point of view, enhancements, upgrades these features:
1. User can create new topic and see it on the same page.
2. Along with the new topic, user can also see number of trivias in each topic.
3. User now gets the page in HTML, as well as JSON formats.
4. User can see the results and feedback of next and previous played trivias by clicking on the next and previous links of the results page.

The main challenges that I came across while working on this project were:
1. Finding the next and previous played trivias data to allow smooth navigation. This was handled by adding an attribute in `Serializer` to hold next and previous data.
2. Loading of all JavaScript files and thus, getting `undefined id` errors for `get` requests while loading other pages. This was handled by writing _page-specific JavaScript_.

Nothing is more fun than working on challenges and nothing gives more joy than overcoming those challenges. The fact that I was able to overcome the challenges, achieve the goal of making end user's experience smooth and yet again, learn a lot from **TriviaZone** project makes me very happy!

Check out the source code of **TriviaZone** [here](https://github.com/soumyaveer/trivia-zone).


