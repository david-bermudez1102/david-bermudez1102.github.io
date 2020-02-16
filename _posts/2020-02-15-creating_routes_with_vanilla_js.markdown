---
layout: post
title:      "Creating routes with Vanilla JS"
date:       2020-02-15 23:31:27 -0500
permalink:  creating_routes_with_vanilla_js
---


For my JS project, I decided to make an app to track workouts and be able to create routines so others can fork them.

It was a very challenging task at first since I didn't have a clear idea of how I was gonna structure my project, especially because I knew my app was gonna be a lot of coding.

But, the real problem came when everytime I wanted to check something new I had done in my project, I had to refresh the page and all of the state in my page was gone!

If I was in a routine/show view and I refreshed, it went straight to the root, and I had to make all of the process...

Luckily, Javascript is awesome enugh to have a method called **History.pushState()**

[https://developer.mozilla.org/en-US/docs/Web/API/History/pushState/](http://)

It takes the state(which is an object), as the first argument, the title of the page(even tho a lot of browsers don't support it) as the second argument and the URL you want to show in the browser as the third paremeter.

And how to implement it?

Well, let's say I stored the fetch data retreived from http://localhost/routines/1 in my Routine class and it created the following object: 

```
Routine: { id:1, name:"Legs Workout", calories:500, exercies:[] }
```

And the page I want to show is http://localhost:8000/routines/1 (Following the same URL pattern all websites should follow).

As you can see, I passed the same id of my object to my route

Of course I'd need a render method for my RoutineRender class. Normally in rails this view would be rendered from the controller explicitly like this:

```
def show
    render 'show.erb'
end
```

routines/show.erb, but in JS it would be something like:

![](https://i.imgur.com/hsephYl.pnghttp://)

This is basically rendering the routine(Of course I have a method called render) to whatever node parent I pass as a target. I am going to pass it to a `<main>` tag as my target(where I want to render).

Now, notice how I also called a method "createRoute()". 

Well, ignore that for a second and let's jump into creating the route with History.pushState().

The first thing that has to be done once you are done rendering your component or whatever you want to render, is to replace the state of your current page like this:

```
(function() {
  window.history.replaceState({intial state object of your application}, null, "");
})();
```

[https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState](http://)

Since there wasn't any state created so far, the inital state should be an empty object, no title and no URL.

Great! Now the state of your app is saved in memory!

Once that my view finishes rendering, I can now push the state

`window.history.pushState({ Routine Object, load: show }, null, "/routines/${this.id}");`

And voilà. the URL changes to **`/routines/${this.id}`**

Notice the object has the key "load". That key can be whatever you want it to be. 

I am basically saying that the state is gonna be my routine object and to load the show() method. 

it is important to pass the method as a callback(No parentheses) Otherwise you'd be calling it and it would throw an error.

Ok. so everything seems to be working, **but what about when you refresh the page?** As you can see nothing happens. Or even worse, if you are not running a server and you opened your SPA from clicking on index.html, it will go to a page that does not exist!

We are just showing a URL to our user like syntax sugar.

Well, to solve that problem, first would be creating a mini server that redirects any path to our index.html. For that I used express.js which is very very very easy to implement.

Just create a file server.js with the following:

```
const express = require("express");
const server = express();

/* route requests for static files to appropriate directory */
server.use("/", express.static(__dirname + "/"));

/* other routes defined before catch-all */
server.get("/x", (req, res) => {
  res.send("ok");
});

/* final catch-all route to index.html defined last */
server.get("*", (req, res) => {
  res.sendFile(__dirname + "/index.html");
});


const port = 8000;
server.listen(port, function() {
  console.log("server listening on port " + port);
});

```
'This is a basic code to create a server that redirects any route to index.html, except for static files.

Make sure to have npm installed and run the following code in your terminal:  `npm install express --save`

Once you are done, run node server.js to start the server and now you can see your page.

Beautiful! Now the server is running in localhost:8000

Going back to our routes, once the server is running and you had pushed the state, add the following line to your code:

```
window.onpopstate = function(event) {
  if (event.state) {
    state = event.state;
  }
  state.load() //Here I call the method inside load once the state is popped or retreived
};
```

Check out the oficial documentation for more info:

https://developer.mozilla.org/en-US/docs/Web/API/WindowEventHandlers/onpopstate

https://willtaylor.blog/client-side-routing-in-vanilla-js/




