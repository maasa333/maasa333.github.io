---
layout: post
title:      "MVC in Sinatra"
date:       2019-10-13 02:45:18 +0000
permalink:  mvc_in_sinatra
---


As I continue on this coding journey, my level of appreciation for all the work that goes into web applications that I mindlessly access has grown tremendously.  I never wondered about the mechanics when using sites such as Facebook.  I mean, all one has to do is simply follow the prompts to create an account, log in, and enjoy all the features that are now magically accessible to them. 

Buuuuuuuuuuuuut, of course, there is no *actual* magic here (at least, not like the ones in Harry Potter).  These web applications we utilize on a regular basis are the result of the blood, sweat and tears (well, maybe not blood) of programmers working behind closed doors, spending hours and hours figuring out methods to ultimately build a tool that the general public can understand and operate with ease.

For example, how is it that when you're on website like Facebook, the display on the screen changes based on what you click?  We can thank **MVC** for that. 

### What is MVC???

MVC stands for Model-View-Controller.  It's a software design pattern to build a framework for web applications.  

The restaurant analogy was very helpful when it came to understanding how MVC works:

```
Restaurant Analogy

Model = Chef 
View = Customer Orders
Controller = Waiter
```

At a restaurant, we have a customer who places an order (View), the chef who is responsible for preparing the requested dish (Model), and the waiter who runs back and forth between the customer and chef, taking and delivering requests (Waiter). 

### How this works in my Sinatra app

For my Sinatra project, I created a web application that keeps a log of dreams that users input.

Here is how the MVC pattern came in to play in order for a user to post a new dream: 

```
class Dream < ActiveRecord::Base
    belongs_to :user
    validates :description, :category, presence: true
end 
```

This Dream class model will create a Dream object with the help of ActiveRecord methods (which I don't have to worry about coding myself because this class is inheriting methods from ActiveRecord).

In order to post a new dream, you will need to fill out a form, which in this case is named `dreams/new.erb` (erb stands for embedded Ruby, and this type of file enables Ruby methods in an HTML form). 

```
<form method="POST" action="/dreams">
    <label for="description">Describe your Dream: </label>
    <br>
    <textarea name="description" id="description" value="<%= @dream ? @dream.description : ""%>" rows="4" cols="50"></textarea>
    <br><br>
    <label for="category">What kind of dream was it?</label>
    <select name="category">
        <option value="">Select One</option>
        <option value="Adventurous">Adventurous</option>
        <option value="Funny">Funny</option>
        <option value="Happy">Happy</option>
        <option value="Scary">Scary</option>
        <option value="Sad">Sad</option>
        <option value="Weird">Weird</option>
    </select>
    <br>
    <input type="submit" value="Save">
</form>
```

A new Dream object gets created based on the inputted information.  In the HTML form tag at the top, we are telling the controller that we want to submit the inputted information to the `"/dreams"` route in the controller. 

```
	    post '/dreams' do
        @dream = current_user.dreams.build(params)

        if @dream.save
            redirect "/dreams"
        else
            erb :'/dreams/new'
        end
    end
```

The method in this route is taking the newly created Dream object, and if it is saved, will redirect to the page that will display all posted dreams, including the new one.

### Now, onward!

Implementing the Model-View-Controller pattern is a simple, organized way to build a web application.  Obviously, there are many more layers to the whole process, but MVC was the most significant aspect to me throughout my learning process in the Sinatra course.

(  ^_^  )
