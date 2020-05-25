---
layout: post
title:      "Top Five! - Sinatra Portfolio Project"
date:       2020-05-25 22:06:05 +0000
permalink:  top_five_-_sinatra_portfolio_project
---


Hey guys, it's that time again where I post a blog about the one of our portfolio projects here in Flatiron's self-paced web development track. This time we are tasked to build a Content Management System (CMS) application using the tools that we've learned so far, including basic html and css.

Deciding what kind of app to build is again the most time-consuming part of the project, with all the apps that currently exist, it's hard to have an idea that is completely unique at this point. So, I just thought of something that people posts on social media that I think has to have it's own application.

Do you ever wonder what other people think what's the best movie they have seen so far? or what games took them out from reality the longest? These types of questions can be answered by asking "what's your favorite thing about this something?" but then people will just give you the one that's on top of their heads, of course. However, we all know that a list is better right? or at least their top five list so that we can actually have a gist of what they like and/or dislike. 

That's where the Top Five! comes in. A simple CMS application that lets users create their top five list of a specific topic and share it to the other users where it can serve as a recommendation as well as a piece of information for those people to know a little something about you.

## The process

Building a Sinatra web application skeleton structure is not easy, you have to make sure you have a Gemfile, Rakefile, an environment where you connect all other files to one another, and then set up a database. Luckily for us, Corneal gem app exists. It basically handles all the things you have to do before starting to write your own code, including a template css file and all the gems that is essential for developing a Sinatra application. More information at [Corneal](https://github.com/thebrianemory/corneal).

After Corneal does its work, the fun begins:
- Make your models and for each, create a database with columns based on their attributes. In my case, I made 3 models (User, Topic, and List).
- Create the appropriate relationship between the models and then run the migrations for your database. After running the migrations, I tested the relationship between the models in 2 ways, using Tux (another gem app) and making database seeds.
- Create views and connect it to the appropriate controllers. I made 3 additional controllers, aside from the application controller that corneal made, one for each models.
- Add user persistence and hide specific actions for users if they are not logged in or a content doesn't belong to them, you don't want anyone to just create, edit, or delete contents that they don't own.
- Add error and confirmation messages for everytime a form was submitted.
- Make sure everything is presentable using css and other controller actions are easy to access by having a navigation bar.
- Clean the codes and enjoy your own creation.

## The project

I used the template stylesheet Corneal gave and did some adjustment to make it somewhat presentable, and here's some snapshot from the application.

![Login page](https://scontent-mia3-2.xx.fbcdn.net/v/t1.15752-9/100635345_609629319668684_8174415335248625664_n.png?_nc_cat=105&_nc_sid=b96e70&_nc_oc=AQkirHiRgCsk8KhiB8AkS-qFyQQ3Em3h7ntCedHppRcF455H3Zfc8wBJmBT6qqPH48ngN6Mh2b42aS94EQB7pl7E&_nc_ht=scontent-mia3-2.xx&oh=1fcf762a1f83819a2a620ad45d2f3e92&oe=5EF10323&dl=1)

![User show page](https://scontent-mia3-1.xx.fbcdn.net/v/t1.15752-9/99436566_663832647510894_8339399494537838592_n.png?_nc_cat=111&_nc_sid=b96e70&_nc_oc=AQmCwjfARUV1q1NvGj-43ARyQGhjY5GDtanvZVuozGZETM3AkjskHI40aIAJap3b93BP4jmDOwy0ekWJjycKslvz&_nc_ht=scontent-mia3-1.xx&oh=6e81a6b7ab12144513a4d93a385661ae&oe=5EF32492&dl=1)

![List show page](https://scontent-mia3-2.xx.fbcdn.net/v/t1.15752-9/100567870_2895009890615807_5986059391185453056_n.png?_nc_cat=105&_nc_sid=b96e70&_nc_oc=AQlm3qcHg8PSarxpWT_IfW53IIb53Err2k1UlrrLGGqTRogbuTOo8m1OrGd07Jb7UUZyYWxvfqOcgfajnKZMoCPE&_nc_ht=scontent-mia3-2.xx&oh=1fd44eeced1d167917d269beac91f074&oe=5EF278C1&dl=1)

That has been what I've learned from the program so far. I'm excited for the new concepts to come and I hope we all make it to the top. Thank you guys for reading! Happy coding!
