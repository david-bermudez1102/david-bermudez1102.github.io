---
layout: post
title:      "Using Fast JSON Serializer – Ruby on Rails"
date:       2020-07-31 03:06:12 +0000
permalink:  using_fast_json_serializer_ruby_on_rails
---


When creating an API, it is very important to serialize the data, so that we only show what it’s needed on fetch requests.

Ruby on Rails has a gem to serialize JSON that doesn’t come by default and it’s called ActiveModel Serializer.

It is great for small APIs, However, if we have nested objects that we’d like to serialize in the same requests, ActiveModel Serializer makes it more complicated.

Fortunately, there are some good gems out there to serialize data. One of the best in my experience is [FastJSON](https://github.com/Netflix/fast_jsonapi). 

It comes with useful features out of the box such as cache, key transformations, collection serialization, links, etc.

To install it, all you have to do is add the `gem 'fast_jsonapi'` to your gemfile, run `bundle install` in your console, then everytime you need a serializer, just run `rails g serializer your_model_name` and it’ll create it for you!

Finally, in the controller, call the serializer from the render method:

`render: YourModelNameSerializer.new(@model_instance)`

That’s it. Just make sure to modify the serializer by passing any attributes you need:

`attributes :id, :name, :lastname`

You’ll be surprised how fast it is compared to ActiveModel’s. In fact, I’ve fetched over 10000 records, with nested objects and everything, and they are rendered in around 40ms using the serializer's cache method combined with Rails cache [Stale?](https://github.com/Netflix/fast_jsonapi) Method.

Besides the speed it offers, one of my favorite features is the key transformation. If you already covered JavaScript, you know it has a camel case convention (e.g. myAmazingFunction()), but in Ruby or Python, the convention is snake case (e.g. my_amazing_function).

When working on large applications, this can lead to unwanted bugs, but luckily it can be fixable by just adding this line to the serializer.

```
set_key_transform :camel_lower
```

Once you refresh, you’ll see the keys transformed!

Check out the documentation to see all the feautures it offers and make the best of your API!

