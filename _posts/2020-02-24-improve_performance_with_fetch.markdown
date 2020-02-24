---
layout: post
title:      "Improve Performance with `fetch()`!"
date:       2020-02-24 00:33:05 -0500
permalink:  improve_performance_with_fetch
---


I find it very helpful to learn concepts through analogies, and the one that stood out to me as I went through this JavaScript unit was the idea of **synchronous** versus **ascynchronous** functions.  Allow me to illustrate!

Currently, I work as a legal assistant which involves completing all sorts of tasks, including making phone calls to schedule appointments.  Let's say that I need to schedule an applicant's deposition.  Oftentimes, I will have to leave a voice message.  Now, one way I could go about proceeding with my task of scheduling this deposition would be to wait for a call back from the other counsel's office with a date, just sitting in my seat and twiddling my thumbs as I wait.   Once I get a response, I can then prepare the notice to be sent out to the parties involved.  But what if the response was delayed due to someone calling in sick?  What if it was an office that was just bad about checking their messages and they take days?  Well, working in this way would be highly inefficient, and I'd definitely get in trouble for not getting more work done.  This is how synchronous functions work, performing one task/function at a time in order.  

A better way to do this task would be to make the phone call and leave a message, but instead of waiting for a response before doing anything else, I could start drafting the notice ahead of time to have it ready to send out as soon as I got a set date.  If it did take days to get a response, I would have gotten other phone calls out of the way and typed up stacks of letters already, so I would be an efficient worker.  This is how asynchronous functions work. 

In JavaScript we use `fetch()` methods to asynchronously retrieve resources from APIs across the network.  So let's say you want to grab resources from a huge database for your application.  Your `fetch()` function would look something like this: 

```
fetch(www.fakeapi.com)
.then(response => {
     response.json()
}
.then(data => {
     doWhateverYouWant(data)
}
```

The url that gets passed into `fetch()` is the API you're wanting to "fetch" data from.  THEN, what gets returned is a Response in HTTP format.  In order to extract the JavaScript Object Notation (JSON) body content from it, we first need to "JSON-ify" this Response by calling `.json()` on it.  THEN, you get a Promise returned as a JavaScript Object, and with this, you can perform further functions to parse that data.

This is a very basic idea of how `fetch()` works, but just know that with this you not only can make HTTP GET requests, but also POST, PATCH and DELETE.   Use this for higher efficiency in your app!
