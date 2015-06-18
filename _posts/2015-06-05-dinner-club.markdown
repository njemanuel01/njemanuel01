---
layout: post
title:  "Dinner Club"
date:   2015-06-5
categories: code
---

# Dinner Club

I created a program that creates a dinner club from a list of names inputted by the user and then stores information on the outings each member went on and how much each member has paid in total as part of the dinner club.  I made a `DinnerClub` class to create the dinner club and store information and a `CheckSplitter` class to calculate the amounts each member added to their total paid.

##DinnerClub

When DinnerClub is initialized, these attributes are set:

```ruby
def initialize(names)
  @names = names
  self.names_hash
  @outings = {}
end
```

@names is an attribute which takes the array of names inputted and using the names_hash method creates the @list attribute which is a hash that stores the names of the dinner club members as keys that point to the total amount they have paid.

```ruby
def names_hash
  @list = Hash.new
  @names.each do |name|
    @list[name] = 0.0
  end
end
```
*meal method*

For each dinner club outing, the meal method takes this inputted data:
	
	-date:  string for the date of the outing
	-location: string for the restaurant attended
	-attendees: array of names for those who attended
	-meal_cost: float value for the cost of the meal
	-tip percentage: int value for the tip percentage used
	-treater: string of the name if someone paid the bill for everyone, default is nil

```ruby
def meal(date:, location:, attendees: , meal_cost:, tip_percentage: 0.18, treater: nil)
  if treater != nil
    charge = meal_cost*(1 + (tip_percentage/100.0))
    add_charge(treater, charge)
  else
    check1 = CheckSplitter.new(meal_cost: meal_cost, tip_percentage: tip_percentage, group:  x = attendees.length)
    charge = check1.cost_per_person
    attendees.each do |name|
      add_charge(name, charge)
    end
  end
  self.outing(date, location, attendees)
end
```
It first determines if the entire cost should be added to a single person, the treater, or if the meal should be split between all the attendees.  If the total cost needs to be split, it calls the CheckSplitter class to find out how much each person owes.  It uses the add_charge method to add either the total amount to one person’s name or if the meal is split, to add the split charge among those who attended.  Lastly, it calls the outing method to store the information of date, location, and attendees in the @outings hash.

```ruby
def outing(date, location, attendees)
  @outings[date] = {location => attendees}
end
```
Outing stores the date as the key which points to a hash that stores the location as a key pointing to an array of members who attended that outing.

When finished, DinnerClub stores the names of each member and the total amount they have paid in the @list hash attribute and the date, location, and attendees information in the @outings hash attribute.

##CheckSplitter

When CheckSplitter is a sub-class initialized by the meal method, its sets these attributes:

```ruby
def initialize(meal_cost:, group:, tip_percentage: 0.18)
  @meal_cost = meal_cost.to_f
  @group = group.to_f
  self.tip_amount(tip_percentage, meal_cost)
end
```
Using these initial amounts, CheckSplitter returns the cost_per_person using the cost_per_person method.

```ruby
def cost_per_person
  self.total_cost / @group
end
```
total_cost is calculated as the meal_cost plus the tip_amount which is calculated as:

```ruby
def tip_amount(tip_percentage, meal_cost)
  @tip_amount = meal_cost*(tip_percentage/100.0)
end
```
