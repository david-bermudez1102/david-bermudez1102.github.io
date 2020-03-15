---
layout: post
title:      "Final Project mode!"
date:       2020-03-15 18:12:28 -0400
permalink:  final_project_mode
---


For my React/Redux project I decided to make a dashboard that can connect to accounting software like [Zoho](https://www.zoho.com/books/) or [Quickbooks](https://quickbooks.intuit.com/).

The app allows an organization to add their own logo, which later will be rendered in the navbar, making it easier to personalize.

Once the organization has been set up by admin, they will be able to add employees, sort records, create their own forms, which later employees are gonna use to store data (invoices, items, contacts, etc).

![](https://i.imgur.com/bgk8dmIl.pnghttp://)

For the example above, I used my partner's business logo and name, and as you can see, the fields can be editable, and they can even connect to another forms(resources), if they are type select or radio.

Every resource can be connected to zoho and/or Quickbooks in order to synchronize the records. 

For example, if the company has a resource of invoices, and it is connected to the zoho api, they can send those invoices periodically.

![](https://i.imgur.com/ErUPknOl.pnghttp://) 

To create an invoice through Zoho Api, it needs to have a customer_id, invoice_number(optional) and line_items. This means the organization needs to create items and customers form, connect them and sync with Zoho in order to retrieve there ids which later will be mapped and send to the external API.

It was challenging at first to model the form builder api, but I figured, rails-wise speaking, a form has many fields, and a field has may values, and so on. 

I had to spend a big time thinking how to map the forms to api keys, until I finally did it!

When it comes to react, I almost didn't have any problems, except with the router that was giving me a bit of a hard time but I figured it out eventually.

This whole idea came from a project I built for the business mentioned above, before I started my journey with Flatiron.

The thing is that project was constantly buggy since I didn't implement best coding practices to make my code more maintainable(It was written with raw PHP and MySQL statements as well as native Javascript).

Luckily, I took advantage of my Rails and React knowledge to make it more general(so other organizations can use it), maintainable and easier to add features constantly. 

Feel free to check out my repo: [https://github.com/david-bermudez1102/enterprise-manager](http://)


