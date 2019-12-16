---
layout: post
title:      "Keep it DRY!!!"
date:       2019-12-16 03:39:15 +0000
permalink:  keep_it_dry
---


Again and again, we are reminded of the sofwater development principle:  Don't Repeat Yourself (DRY). 

As programmers, this is an important rule to live by.  Not only does your code visually look nicer, but there is also much less room for errors. 

Let's compare two code snippets that perform the same function.  I will use  the `DreamsController` from my Rails web application, displaying only the pertinent lines of code for the purpose of explaining how I applied the DRY principle here: 

Original Version: 

```
class DreamsController < ApplicationController
    
   def new
      *code here*
   end
    
   def create
      *code here*
   end

   def show
      @dream = Dream.find_by(id: params[:id])
      *code here*
   end

   def index
      *code here*
   end 

   def edit
      @dream = Dream.find_by(id: params[:id])
      *code here*
   end

   def update
      @dream = Dream.find_by(id: params[:id])
      *code here*
   end

   def destroy
      @dream = Dream.find_by(id: params[:id])
      *code here*
   end
end
```

As you can see, the line `@dream = Dream.find_by(id: params[:id])` is used several times in this controller.  Technically, it will work just fine, but visually this does not look so pretty.  As soon as you see repetitive lines, you should automatically think of it as an opportunity to DRY off your code!

In this scenario, a new method can be created for the purpose of setting an instance of `@dream`: 

```
   def set_dream
      @dream = Dream.find_by(id: params[:id])
   end
```

Now, I can use a Rails "filter" method to have this `set_dream` method run before every action within the `DreamsController`.  For this to work, I place this line of code at the very top of the controller: 

```
before_action :set_dream
```

This is great, but wait!  I don't actually want to be setting a dream before **every** action.  Conveniently, I can set limitations to where I want the `before_action` to take place.   I updated this line to set the `before_action` to all actions except for `new`, `create` and `index`:

```
before_action :set_dream, except: [:new, :create, :index]
```

*(There is also the option of setting a `before_action` for `only:` and `around:`, but for the purposes of this controller I went with `except:` because there were fewer exceptions.)*

The resulting `DreamsController` now looks as follows:

```
class DreamsController < ApplicationController
   before_action :set_dream, except: [:new, :create, :index]
    
   def new
      *code here*
   end

   def create
      *code here*
   end

   def show
      *code here*
   end

   def index
      *code here*
   end 

   def edit
      *code here*
   end

   def update
      *code here*
   end

   def destroy
      *code here*
   end
	 
   def set_dream
      @dream = Dream.find_by(id: params[:id])
   end
end
```

Much better!  

Just remember, this is just one out of several ways to go about DRY-ing up your code. 

v(  ^_^ )v
