---
layout: post
title:      "The beauty of React and building my own JSX like library."
date:       2020-03-23 17:41:04 +0000
permalink:  the_beauty_of_react_and_building_my_own_jsx_like_library
---


When I first started my journey with Flatiron I was skeptical to use JS based fontend frameworks or libraries (like Jquery) because I felt everything is made easier for anyone who uses them, and with time, basics learned would be forgotten. 

What if I learned Javascript, but started using JQuery and all of the sudden I have a bug that JQuery can't fix, and I forgot the Javascript bases since I've been using JQuery only? Well, I could debug for sure, but it would take me longer for sure.

But with React ,it is different, because  I can still build my own functions and still play with objects and variables and it feels like I am using plain JavaScript, which I love.

That's not all I like about React. The fact that I can use the JSX syntax, makes me feel more like I was still developing my front end with pure html, making my code way easier to maintain and it really isn't hard to understand how [JSX compiles to JavaScript code](https://reactjs.org/docs/introducing-jsx.html).

```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

Compiles to:
```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

Normally, with plain JS, you could simulate the same using backtics :

```
const element = `<h1 class="greeting">
                                            Hello, world!
                                    </h1>`
);
```

But there are a few limitations with this. For example, the loading time would take longer (since Javascript has to parse it to JavaScript everytime the page is reloaded), and if I wanted to add content dynamically to that element, I could use something like innerHTML, but that would make the whole element to be parsed again and re-rendered.

This works fine for a small app, maybe a personal page, but definitely not for big projects, since the DOM is what uses more memory on browsers.

Also, it just doesn't look great in your code and it's hard to format:

![](https://i.imgur.com/kY4Mun2.pnghttp://)

Which leads to a much better plain Javascript tool: [document.createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

```
const element = document.createElement("h1")
    element.className="greeting";
    element.append(`Hello, world!`);
);
```

Now there's more control with the nodes I create.

Let's say I had 2 timers. One that updates every second and the other one every 5 seconds and they both are appended to my element in different times. The fact that I am using the native API, makes my first counter to be counting independetly from the second counter, which make it more efficient since I am not updating the entire element. Just what needs to be updated.

Of course, it also comes with a lot of limitations. Imagine you had a div container, with a lot of elements nested in it? Well, it's definitely doable using createElement, but the code would become messy and harder to maintain and debug.

That's why JSX is one of my favorite things from react. But what if I wanted a plain Javascript app that doesn't require lots of state or bunch of features?

The solution would be creating your own [virtual dom](https://stackoverflow.com/questions/21965738/what-is-virtual-dom).

In fact, for my Javascript and Rails final project, I needed something efficient to make the DOM easier to handle, since I was noticing my app was becoming larger as I added more features, so I decided to implement a class that would create my nodes, and nested nodes:

```
class Elem {
  static create(tagName, attributes, ...append) {
    const elem = document.createElement(tagName);
    Object.keys(attributes).forEach(attribute => {
      elem.setAttribute(attribute, attributes[attribute]);
    });

    append.forEach(a => elem.append(a));
    return elem;
  }

  static render(target, remove, ...components) {
    if (target) {
      if (remove) target.innerHTML = "";
      components.forEach(component => {
        if (component) target.append(component);
      });
    }
  }
}
```

That piece of code makes it easier to build my nodes with Javascript:

```
const element = Elem.create(
      "div" // tag name
      { class: "d-flex display-4 mt-4 text-justify", style: "font-size:20px;" }, //Props or attributes
      "Example string", //A nested piece of text
      Elem.create("div", null, "Another div") // A nested div with no props
    );
```

It definitely looks easier when it comes to building nodes, but it wasn't enough for me. Before I learned react, I saw the JSX syntax and I really liked it. 

In fact, I liked it so much that I built my own JSX-like parser(Which compiles in the code above) and used it to make my code cleaner. You can check it out [here](https://github.com/david-bermudez1102/elementX).

I used fetch to read the files and Regex to parse the files, and it can be used to write html directly into Javascript. Once the code is compiled in the browser, a link to the compiled code for production is generated.

Of course, it is no react, but definitely useful if it's used for small to medium size projects or for beginners to react that want to understand the compiling process.

In the meantime, I'll keep enjoying all the benefits of react like fast development, state management, etc, while I also maintain my library and keep adding things to make web development easier.
