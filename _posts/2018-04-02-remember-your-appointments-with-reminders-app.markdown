---
layout: post
title: Reminders - Manage your appointments
date:  2018-04-02 18:10:00
categories: main
banner_image: "reminders.png"
summary: Your personal assistant to help you manage your important tasks. Never miss another appointment again!
---

Do you often find yourself forgetting the birthday of a loved one? Or worse, your own wedding anniversary? Speaking from my personal experience this can be a huge problem. **Reminders** app is the solution to these problems. This app will let you manage your appointments and send notifications to yourself and others well in advance.
 
  Interesting, but what features do I get with this app?
  
  **Reminders** comes with following features:
  1. Viewing all Reminders
  2. Adding a new reminder
  3. Updating a reminder
  4. Setting the time for the email notifications.
  5. Setting the email addresses of the recipients, who need to receive the email notification.
  6. Deletion of the reminder.
  
  
  **Reminders** app is a _Rails_ API with _React-Redux_ frontend. Rails takes care of data manipulation and persistence and React is responsible for displaying the data and sending fetch requests for create, update or delete. The routing is done using `react-router`. Scheduling of email notification is done using _Sidekiq_, which enqueues the jobs when the reminder is created and removes it once the reminder is deleted.
  
  While working on this project I came across many challenges, form which I learned a lot: 
  1. I wanted to save the recipients email addresses in form of an array in the database. I was able to overcome this difficulty by using the array feature in PostgreSQL. 
  2. Integrating Rails API with React frontend. 
  3. Displaying new and edit form on the same page. 
  4. Redirecting to the Home page after deletion of a reminder. 
  
 Working on this app was a great learning experience and a lot of fun. Other than the few challenges listed above, I came across many more issues, which required many hours of debugging, fixing the code and reading materials from different resources. In the end, I am very happy to see the final product. I absolutely loved working on this project.
 
 Check out the source code of [**Reminders**](https://github.com/soumyaveer/reminders) 
