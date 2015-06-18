---
layout: post
title:  "Coding: A Reflection on Creation"
date:   2015-06-21
categories: reflection
---

#Coding: A Reflection on Creation

A few days into class I noticed that my teacher in coding used the word "create" a lot.  We create programs, we create classes, we create methods, create, create, create.  It got me thinking about the notion of creation.  Specifically, why do we create things, what does it mean to create, and what is a creator?  A further question that kept coming up is, what does it mean to create something with free will (or that can deviate) from the intentions of the creator?  Here's my foray into these questions.

##What does it mean to create? and Why do we create?

These two questions seemed intertwined to me so I thought I'd tackle them together.  As coders, we create code to achieve some desired end.  In the end, it all boils down to writing a program that either stores data in some way, or runs some sophisticated set of algorithms on the data (maybe not so sophisticated in my case) to achieve a purpose.  We write "code" to do "things." We create so that our creations achieve a desired end.  We make sure that there is a structure to the program so that when it gets "A", it returns a desired "B."  Contrast this thinking with that of a writer.  Specifically a writer who writes things that no one else will ever read or even see.  Since this writer's work will not achieve a tangible "end", is he/she any less a creator?  I would argue no, that in fact this writer's work is achieving it's desired end even though no one else even knows it exists.  In the writer's case the desired end is the writing itself, for the writing itself is an expression of the writer's own thoughts, feelings, and desires.  And that expression is itself a creation.  Have you ever had a piece of code/program that you just had to test out even though it what completely useless?  If so, welcome to the life of the starving artist.  Keep in mind though, that the writer just like the "coder" needs to add some type of structure to his/her thoughts, feelings, and desires, for it to be creative.  It's not enough to just have a thought (I think about story lines all the time but have very few actual created stories).  Creation of something requires that structure be imposed just in the same way a "coder" will impose structure/logic upon his/her program.  So what does it mean to create?  I would say that to create is to express our thoughts/feelings/desires in some structured form.  Why do we create?  To achieve some desired end.

##What does it mean to be a creator?



##change.rb

The Change class allows the user to access a list of changes that have been made to the database as well as a list of changes that only the current user has made to the database.  The method returns an Array of Hashes with information on the changes the current user has made.

```ruby
def self.where_user(user_id)
  CONNECTION.execute("SELECT * FROM 'changes' WHERE user_id = ?;", user_id)
end
```

##Questions to reflect and comment on:
1.  Are we an instance of creation?
2.  For those who said yes to #1, why?  And before you answer because it's in the Bible, go back to Genesis and reread all that goes on there in Creation.  There is so much more if you really ponder/pray about it.
3.  For who who said no, why not?  If we ourselves are not created, where does our creative nature come from?  For that matter, where does our existence come from?  (I'm no being combative here, I really would like to hear your honest answer)
4.  If we as humans are free, free to choose, free to create, how does that free will affect Creation? 
