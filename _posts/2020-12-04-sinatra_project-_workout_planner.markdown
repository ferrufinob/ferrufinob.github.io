---
layout: post
title:      "Sinatra Project- Workout Planner"
date:       2020-12-04 19:03:30 -0500
permalink:  sinatra_project-_workout_planner
---


For my Sinatra project I wanted to make something would make my life or someone elses life easier. I love organization and planning. At the moment I write all of my workouts in a calendar, and wish there was a better way to plan them. For my Sinatra application, I decided to make an application that would help plan weekly workouts. I needed to implement everything that I had learned for the current module (MVC, CRUD, ActiveRecord, SQL, RESTful routing). 

First came the project directory set up which had to be in MVC structure, this structure provides separation of concern and separates our application into three components: 

* Model: handles data and the logic(where our data is saved and manipulated)
* Views: is the graphical interface/ what our user will see(HTML)
* Controllers: is the user interface which  sits between our model and the view and interacts with the database(it 'GETS' us this data). This is where we will be defining our routes
 
With separation, our user requests are handled as follows:

1. the client sends a request to the server and is routed to the appropriate Controller
2. the Controller retrieves that data it needs from the model to be able to respond to the request
3. the Controller then gives the data it retrieved data to the View
4. the View is rendered and then sent back to the client for it to be displayed to the client in the browser.

Secondly, I had to set up my tables and models, I decided on two tables: users and workouts

* users would have a name, email and password. For my model association a user would have many workouts
* workouts would have a date, target area, activity and target type. My for my model association workouts would have many users. For the beginning of my project I had 3 models(an exercise model), as time progressed I hated it. I did not want reps or sets since I do timed workouts, I just wanted one textbox area where I could type my activity for that day(something flexible and simple). I found having two models worked best for me.

Third, I had to set up my controllers. I needed to make sure users are able to Create, Read, Update, and Delete their workouts as well as their user account. I had alot of fun playing around with my forms trying to figure out ways to hijack other users workouts and finding ways to prevent that from happening, the last thing we want is someone else being able to access our users information or even worst try to modify it.  
 One of the things that I struggled with the most was figuring out whether to redirect or render a view. 
Some things that helped me decide whether to redirect or render:
1. You render a form(new/edit), and are able to access any instance variables that you pass through that controller action.
2. When redirecting you are creating a new http request, therefore we are unable to pass any instance variables(stateless). 

Lastly, the views. We needed to be able to make sure our users were able to READ their workouts. I was able to do this by giving my corresponding view access to instance variable through its controller action. Overall, my Sinatra project was alot less stressful to build than my cli project. I loved how quick and simple it was to create an application with Sinatra and looking forward to using Sinatra to build many more applications. Very excited to start learning rails and seeing what I can create with it.





