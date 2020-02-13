---
layout: post
title:      "Creating Gymmate Javascript App"
date:       2020-02-13 20:41:58 +0000
permalink:  creating_gymmate_javascript_app
---

For my JS project I decided to make an app to track workouts and also being able to sign up as a trainer and create multiple routines where gym goers can add them to their workouts list.

For my rails API, I chose the models User, Trainer, Program, Exercise, etc. and also implemented some polymorphism, since I had 2 account types (trainer and gym goer).

Building the API wasn't hard at all, except for serializing the JSON, which wasn't really complicated, it just took longer.

Once I had my API ready I chose the same MVC pattern I used for rails to start coding my front end.  Basically, for every model in rails, I created a JS file and put it on my index.html file

```
class Trainer extends Account {
  constructor() {
   
  }

  static create(json) {
  }
}

//===============================================================================//

class TrainerView {
  constructor(trainer) {
    this._trainer = trainer;
    this._form = TrainerForm.create(this);
  }

  static create(trainer) {
    return new TrainerView(trainer);
  }

  get trainer() {
    return this._trainer;
  }

  get form() {
    return this._form;
  }


}

//===============================================================================//

class TrainerForm {
  constructor(view) {
    this._view = view;
  }

  static create(view) {
    return new TrainerForm(view);
  }

  get view() {
    return this._view;
  }

  get trainer() {
    return this._view.trainer;
  }
}

//===============================================================================//

class TrainerRender {
  constructor(trainer) {
    this._trainer = trainer;
  }

  static create(trainer) {
    return new TrainerRender(trainer);
  }

  get trainer() {
    return this._trainer;
  }
}

//===============================================================================//

class TrainerController {
  constructor(trainer) {
    this._trainer = trainer;
  }

  static create(trainer) {
    return new TrainerController(trainer);
  }

  get trainer() {
    return this._trainer;
  }

  create() {}

  show() {
  }

  update() {}

  delete() {}
}

```

I used the same pattern for all of my models, encapsulating the views in the modelView class, forms in the modelForm class, etc.... 

To be honest I came to this pattern after having lots and lots of code and couldn't be happier about separating my  components from my rendering and from my objects

When it came to creating components, it was exhausting having to create a constant, then call createElement to create the component and append everytime I wanted to render, so I came up with a perfect solution

![](https://i.imgur.com/c3q88sx.png)

That's right! I made a class called Elem, with a method "create" and I pass the attributes as an object, the handler and last but not least an array of more components.

Instead of doing something like:

```
workout() {
  const div = document.createElement("div")
  div.id = id
	div.className = class
	div.append(another component...)
}
```

I can just do 

```
workout() {
  return Elem.div({id:"my_id", class:"margin-0", etc..}, null, Elem.h2(..), ... As many attributes as I want
}
```

It looks much more organized and no need to instanciate variables when there is no need to. Easier to modify and read too.

In conclusion, Javascript is a powerful language and I love it, but unfurtunately, when it comes to making a big project (such as mine), code mantainability and readability can become a quite messy if you don't properly encapsulate everything.

Here are some small pictures of what my JS app looks like (Everything rendered through virtual DOM. Even forms!)

![](https://i.imgur.com/azbCOYnl.png)
![](https://i.imgur.com/XQ4MuWSl.png)
![](https://i.imgur.com/a64WtRxl.png)


