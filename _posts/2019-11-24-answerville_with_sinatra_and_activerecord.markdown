---
layout: post
title:      "Answerville with Sinatra and ActiveRecord"
date:       2019-11-24 17:09:41 +0000
permalink:  answerville_with_sinatra_and_activerecord
---


I created a portal where you can ask any kind of questions and receive answers from all around the world! All made with Sinatra, ActiveRecord, HTML and some Bootstrap!

[https://github.com/david-bermudez1102/answerville-sinatra-app/](http://)

The idea was actually based on all the questions I had about this project. "Why not creating something where I can just ask any kind of questions I want?". Once I decided this is what I wanted to do, I started writing down my objects first in a simple notepad.

![](https://i.imgur.com/MxTrSVB.png)

That's right! I wanted something sort of a small social network where people can follow other people, give likes to posts, answer many questions, etc.

And that's how I came up with the name "Answerville". It took me around 3 hours to come up with it, but I did it! Now time to start coding.

![](https://i.imgur.com/sht9NZK.png)

The migrations and models were the easiest to create, except for the followers part, since a user can be a follower and can follow many people!

Luckily for me, I found this very well explained article that helped me to understand this type of relation better 

[https://medium.com/@esmerycornielle/making-a-followers-feature-with-ruby-on-rails-and-active-record-ddb3d1dda060](http://)

Once I resolved that part, I started testing with tux and creating my views and controllers. I made the most basic forms at first to make sure it was working, and when I finished it, I started styling my page with Bootstrap. 

Adding Bootstrap to my project was what took the most, but not really hard to do. 

To summarize, Everything took me around a week to do and now I have a beutiful site called Answerville and this is how it looks!

![](https://i.imgur.com/vixpZgm.png)

![](https://i.imgur.com/pC1bUYq.png)

![](https://i.imgur.com/w0I9INx.png)

I will be deploying the project on [http://answerville.us](http://) eventually for more details. In the meantime, feel free to check out my project on github.
