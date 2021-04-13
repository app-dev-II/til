---
layout: post
title: Things I learned from The Ruby Koans
---

Things I learned from [The Ruby Koans](http://rubykoans.com/):

### Shovel Operator Behavior
Most things in Ruby behaved as I would have expected.  The only code that threw my off was the test below.

```ruby
   def test_the_shovel_operator_modifies_the_original_string
    original_string = "Hello, "
    hi = original_string
    there = "World"
    hi << there
    assert_equal  "Hello, World", original_string

    # THINK ABOUT IT:
    #
    # Ruby programmers tend to favor the shovel operator (<<) over the
    # plus equals operator (+=) when building up strings.  Why?
  end
```

I understand why programmers tend to favor the shovel operator over the plus equals operator.  I found this interesting analagy on StackOverflow.

> You have a glass of water that is half full and you need to refill your glass.
> 
> First way you do it by taking a new glass, filling it halfway with water from a tap and then using this second half-full glass to refill your drinking glass. You do this every time you need to refill your glass.
> 
> The second way you take your half full glass and just refill it with water straight from the tap.
> 
> At the end of the day, you would have more glasses to clean if you choose to pick a new glass every time you needed to refill your glass.
> 
> The same applies to the shovel operator and the plus equal operator. Plus equal operator picks a new 'glass' every time it needs to refill its glass while the shovel operator just takes the same glass and refills it. At the end of the day more 'glass' collection for the Plus equal operator.
 
This makes sense, and I am all about writing more efficient code.  What surprised me was that by using the shovel operator on `hi << there` above, it also moidifies the `orignal_string`. In order to understand why this was, I had to take a deeper look under the hood of Ruby to understand how it treats objects. 

```shell
3.0.0-p0 :001 > original_string = "Hello, "
 => "Hello, " 
3.0.0-p0 :002 > original_string.object_id
 => 260 
3.0.0-p0 :003 >  hi = original_string
 => "Hello, " 
3.0.0-p0 :004 > hi.object_id
 => 260 
3.0.0-p0 :005 > there = "World"
 => "World" 
3.0.0-p0 :006 > there.object_id
 => 280 
3.0.0-p0 :007 >  hi << there
 => "Hello, World" 
3.0.0-p0 :008 > hi.object_id
 => 260 
3.0.0-p0 :009 > original_string.object_id
 => 260 
3.0.0-p0 :010 > original_string
 => "Hello, World" 
```
Since the shovel operator modifies the original variable of `hi`, it in turn will modify any variable that shares the same object id as `hi`, namely `original_string`.  Going through this same excercise using the += operator below, we see that this actually creates a new object id for `hi`, thus it does not modify the original object id, and in turn doesn't modify the `original_string`.

```shell
3.0.0-p0 :012 >  original_string = "Hello, "
 => "Hello, " 
3.0.0-p0 :013 > original_string.object_id
 => 300 
3.0.0-p0 :014 >  hi = original_string
 => "Hello, " 
3.0.0-p0 :015 > hi.object_id
 => 300 
3.0.0-p0 :016 > there = "World"
 => "World" 
3.0.0-p0 :017 > there.object_id
 => 320 
3.0.0-p0 :018 >  hi += there
 => "Hello, World" 
3.0.0-p0 :019 > hi.object_id
 => 340 
3.0.0-p0 :020 > original_string
 => "Hello, " 
3.0.0-p0 :021 > original_string.object_id
 => 300 
```
