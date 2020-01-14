---
layout: post
title:      "My First App in Rails!"
date:       2020-01-13 17:35:50 -0500
permalink:  my_first_app_in_rails
---


For my final project I decided to make @nswerville. The same App I made in Sinatra in a more abstract and simplified way.

The main purpose of @nswerville is to let users ask questions in a easy way and get responses from anywhere around the world. So far, the app has features like asking, answering a question, following users, like a question, like an answer, etc. And this was all made in a short period of time thanks to the powerful Ruby on Rails Framework.

The use of rails made it easier for me to make all the migrations, controllers, models, etc. 

Even tho rails is very powerful, I still spent a lot of time refactoring the old code I wrote for my Sinatra App to rails helpers.  

For instance, the code for my login view in Sinatra looked like this:
```
<div class="col-md-4">
  <% if flash[:error] %>
  <div class="alert alert-danger">
    <%=flash[:error]%>
  </div>
  <% end %>
  <% if flash[:success] %>
  <div class="alert alert-success">
    <%=flash[:success]%>
  </div>
  <% end %>
  <div class="card bg-transparent border-0">
    <div class="card-header text-light border-0" style="background-color: rgba(0,0,0,0.1);">
      <div class="row">
        <div class="col text-center">
          <h1 class="card-title display-4">
            <i class="fa fa-sign-in" aria-hidden="true"></i>
            Login
          </h1>
        </div>
      </div>
    </div>
    <div class="card-body bg-transparent text-light px-0">
      <form action="/login" method="POST">
        <div class="form-group list-group-item border-0 px-5" style="background-color: rgba(0,0,0,0.1);">
          <label class="form-label display-4" style="font-size:22px;" for="username">Username</label>
          <input class="form-control form-control-lg" type="text" name="username" id="username" placeholder="Your username">
        </div>
        <div class="form-group list-group-item border-0 px-5" style="background-color: rgba(0,0,0,0.1);">
          <label class="form-label display-4" style="font-size:22px;" for="password">Password</label>
          <input class="form-control form-control-lg" type="password" name="password" id="password" placeholder="Your password">
        </div>
        <div class="form-group list-group-item border-0 text-center" style="background-color: rgba(0,0,0,0.1);">
          <input class="btn btn-lg send-btn" style="color:#fff;border:2px solid #fff;" type="submit" value="Login">
        </div>
        <div class="form-group list-group-item border-0 text-center" style="background-color: rgba(0,0,0,0.1);">
          <small><a href="/signup" class="card-link text-light">Don't have an account? Sign up here.</a></small>
        </div>
      </form>
    </div>
  </div>
</div>

```

While the same Login form in Rails was separated in a partial "_form.html.erb" and the actual view "new.html.erb"

*_form.html.erb*
```
<%= form_with model: user, url:login_path do |f| %>
  <%= form_group f, user, :email, "Enter your email" %>
  <%= form_group f, user, :password, "Enter your Password" %>
  <%= content_tag :div, class:form_group_class+form_group_class_with_buttons do %>
    <%= f.submit "Login", class:login_button_class %>
  <% end %>
  <%= content_tag :div, class:form_group_class+" text-center" do %>
    <%= link_to "Don't have an account? Sign up here.", signup_path, class:card_link_class+"small" %>
  <% end %>
<% end %>
<%= render 'layouts/social_options' %>
```

*new.html.erb*
```
<% title "Login" %>

<%= content_tag :div, class:"col-sm-auto", style:"width:500px" do %>
    <%= render partial: 'layouts/errors', locals:{model:@user} %>
    <%= render 'layouts/flash_message' %>

    <%= card do %>
        <%= card_header do %>
            <%= cell do %>
                <%= card_title :h1, icon:"fa-sign-in", label:"Login" %>
            <% end %>
        <% end %>

        <%= card_body class:"login_card_body" do %>
            <%= render partial: 'form', locals:{user:@user} %>
        <% end %>
    <% end %>
<% end %>
```

As you can see both codes produce almost the same form but it looks more organized and understandable the rails way. Of course, I am also rendering a partial "_social_options.erb"  which contain the buttons to login through social media. I rendered the same partial in the Signup page (users/new.html.erb) for abstraction purposes.

Rendering partials in rails is a very powerful tool for your rails app and it makes your code very DRYed. I used it a lot through the entire development.

Regarding the design of the app, I kept using bootstrap and font-awesome. At first, I used the same old design as in the Sinatra project:

![](https://i.imgur.com/vixpZgm.pnghttp://)

But I chose to make a more freiendly UI. It was a very challenging task to change the style of the website, but with the help of rails helpers, partials, callbacks, etc, I made it happen and now my app looks like this:

![](https://i.imgur.com/GqPgwIj.pnghttp://)

With Rails I can put all of my classes on Helpers in a more organized way than Sinatra's:

![](https://i.imgur.com/Brd30e0.pnghttp://)

FInally, after refactoring the whole project on rails, creating the appropriate controllers, models, migrations, etc. I went ahead and started the login feature with omniauth.

I gave users 3 choices: Facebook, Google and Github Login. It was a bit difficut to handle the part when users had the same email in all of the apps, due to the email uniqueness validation, but I figured if the user already has an existing email, it will just ask them to sign in with that account instead.

Once the user is validated and signed up through a third party, they can modify their @nswerville password, just in case they didn't have access to any of their media account.

Feel free to check my GitHub Repo for a better understanding of my project:
[https://github.com/david-bermudez1102/answerville-rails-app](http://)


