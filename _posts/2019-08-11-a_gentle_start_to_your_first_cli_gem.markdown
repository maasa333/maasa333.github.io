---
layout: post
title:      "A Gentle Start to Your First CLI Gem"
date:       2019-08-11 14:23:15 +0000
permalink:  a_gentle_start_to_your_first_cli_gem
---


The time has come.  It's been a couple of months into the Flatiron program and you now face Portfolio Project #1.  The task of creating your very own Command Line Interface Gem now looms before you.  There is no lab with rspec tests waiting to be passed, and no multiple choice quiz here.  This is the moment for you to build something **from scratch.** 

At this point, you might be excited about taking on a challenge that will test your knowledge and allow your creativity to enter the picture.  Perhaps you feel nothing at all, simply approaching this as another task to be completed to proceed to the next level.  Or maybe you're like me, feeling utterly terrified and discouraged, wondering how the heck you'll be able to overcome this daunting obstacle.

My first thought was, "How am I supposed to even start this??  I can't remember all those folders and files that need to be used!!!!"

You've probably noticed by now that Ruby has some pretty handy tools that make coding life easier.  WELL, 'turns out there is a *beautiful* RubyGem that can jumpstart your project for you!

To start off, go into the brand new blank file, either on IDE or in your local environment, and run the following in the terminal:

```
bundle gem <the name of your project>
```

*(You do not include the `<` and `>` symbols here.)*

If your project name consists of more than one word, I would recommend that you use Snake case (underscores) as opposed to hyphenating (dashes):

`my-awesome-gem`  =>  `my_awesome_gem`

This might not seem like a big deal, but it could really save you from having to do some extra work.  Using hyphens when entering `bundle gem` will create new Module files instead of compiling everything at one level.  So if your project name was `my-awesome-gem`, you would end up creating a file named `my`, a file within that one called `awesome`, and at the third level a file named `gem`, which wouldn't make much sense for the purposes of this project.  

After hitting the `enter` key, you should see the following pop up in your terminal:

```
// ♥  bundle gem my_awesome_gem
Creating gem 'my_awesome_gem'...
MIT License enabled in config
Code of conduct enabled in config
      create  my_awesome_gem/Gemfile
      create  my_awesome_gem/lib/my_awesome_gem.rb
      create  my_awesome_gem/lib/my_awesome_gem/version.rb
      create  my_awesome_gem/my_awesome_gem.gemspec
      create  my_awesome_gem/Rakefile
      create  my_awesome_gem/README.md
      create  my_awesome_gem/bin/console
      create  my_awesome_gem/bin/setup
      create  my_awesome_gem/.gitignore
      create  my_awesome_gem/LICENSE.txt
      create  my_awesome_gem/CODE_OF_CONDUCT.md
Initializing git repo in /mnt/c/Users/konom/my_awesome_gem
Gem 'my_awesome_gem' was successfully created. For more information on making a RubyGem visit https://bundler.io/guides/creating_gem.html
[01:29:25]  konom 
// ♥ 
```

Tadaaaaahhh!!!  Just like that, you've got folders for `bin` and `lib`, not to mention a Code of Conduct and license document!  Like a wizard/witch performing magic, you've conjured up a nearly perfect setup for you to get to work!  Just need a few tweaks here and there (particularly in the `gemspec` file), and you can focus on the main task at hand. 

Hopefully, taking this first step successfully has calmed down any anxiety you may have felt at the very beginning of the project. 
 
As you continue on, try to keep your process as simple.  It's perfectly okay to first use fake data to stub out your code, in order to make sure that your files are properly communicating with each other.  Once your mock CLI Gem is working the way you intend it to, you can then scrape the real data, and add additional functions if you want to.

Finally, I will leave this here:

```
if stuck_on_a_problem
   research_error_on_google
elsif
   ask_for_help
else
   TAKE_A_BREAK
end
```

**You can do this!  Have fun!**
