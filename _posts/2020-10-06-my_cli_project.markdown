---
layout: post
title:      "My CLI Project"
date:       2020-10-06 12:49:30 -0400
permalink:  my_cli_project
---


The idea of creating something from nothing was frightening. I was no longer going to have labs tests guiding me and instead had to figure out on my own how to get my code working. Also the idea of having to explain my code to someone was scary as well, my brain blanks out once I am on the spot, BUT this will be great practice for me to prepare for future interviews. I want to be as prepared as possible and get over my fear of presenting. For our first project we were asked to collect data from a website either by scraping or using an API. Not feeling completely comfortable with API's or finding an API that I liked, I decided to go with scraping. I am always looking for recipes so I decided to scrape my favorite vegetarian recipes website. It will be something I will actually use for myself, my biggest pet peeve is going to a recipes web page and having to scroll through a mountain of pictures and information just to get to the recipe. With my app I wanted the user to be able to get straight to the instructions/ingredients. 

If you decide to scrape a website, a great way to check and see if it's scrapable is to check the /robots.txt file. This [guide](https://varvy.com/robottxt.html) came in handy, it tell's you what can be scraped without getting blocked from the website.

I spent 2 days trying to scrape my website but I later discovered that there were some recipes with completely different class attributes, that was not going to workout. So I searched and searched and finally landed on a different website [Skinnytaste](https://www.skinnytaste.com/). FYI don't build your gem until you have completely decided on a website/project name, I found out later on that I couldn't change my gemfile name so I had to create a brand new gemfile and transfer all of my coding into that one.

For my CLI I created 4 classes:

* CLI class: this will be the user interface

* Course class: I created this class method because a course has many recipes. This class method will hold an @recipes instance variable that will hold related recipe objects, this object will know about the recipe objects but it will not know about the recipe attributes. I initialized it with a name and ref attribute accessor. the ref accessor will be helping me by providing a reference point that will lead me to the recipe page belonging to the course. 

* Recipe class: I gave this class method an course attribute accesor, this will help me link to a course object. Also added @ingredients and @instructions instance variables that will be holding recipe details. I initialized with a name, course and url. 

* Scraper class: In this class method I will be pulling all the data I need such as the courses, course link that leads to that courses recipes and the link that leads to the individual recipe to scrape the ingredients/instructions.

Getting my code to work was trial and error. Two of my biggest struggles were getting the right attributes and linking everything together to display the right information to the user at the right time. My first error was figuring out how to get inside the courses to access the recipe names. I didn't realize till later that the reason why my code didn't work was due to me not providing the correct way to get that link. This is when I created a :ref attribute to save the url for the courses so that I could get inside that page and be able to call that :ref in my self.scrape_recipe method. This project made me realize how important pry is, just throw a binding.pry at the code that seems to be giving you a problem and it will tell you exactly what is behind your code.
My biggest mistake was not working on my CLI class first.  I had created my other class methods and methods inside of them but didn't quite plan out how they would be displayed in the CLI. 
The first week of this project tested my knowlede of object orientation, I didn't think I was going to be able to complete this project but I didn't want to give up, but I proved myself wrong. This project helped me understand how the self works and how to establish object relationships. 
I can't wait to see what the future lessons and projects have to bring. My advice for completing this project is to throw a binding.pry for every step and to break your code into small steps, don't try to write as much code as possible and not test to see if it works first.(another mistake I made)










