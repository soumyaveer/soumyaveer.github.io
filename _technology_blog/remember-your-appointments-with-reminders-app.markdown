---
layout: post
title: Reminders - remind yourself and others like a Boss! 
date:  2018-04-02 18:10:00
categories: main
banner_image: "reminders.png"
summary: Your personal assistant to help you manage your tasks. Never miss another appointment again!
---

Do you find yourself forgetting birthdays of loved ones? Or worse, your own wedding anniversary? Speaking from my personal experience, this can be a huge problem. The **Reminders** app is the solution to this. It lets you setup email reminders for important tasks.
 
Interesting, right?, lets see what all this can do:
  
  1. Setup and manage reminders
  2. Setup the time for the email notification for the reminder.
  3. Setup people who need to be notified.
  
  **Reminders** app is based on a Rails backend, with React on the frontend. To be more specific, Rails handles data persistence and the delivery of notifications (via Sidekiq). It exposes the data via an API to the frontend. The frontend uses React, Redux for state management and `react-router` for routing. 
  
  This project was fun, as it was the first time I was using Rails as a API server. React, Redux, react-router helped me model and build a richer user interface, which otherwise would have been complicated.
   
 Other than all the fun mentioned above, I came across various issues, which required hours of debugging and learning from various sources on the internet. In the end, I am very happy to see the final product. Looking forward to doing more with this stack.
 
 Check out the source code of [**Reminders**](https://github.com/soumyaveer/reminders) 
