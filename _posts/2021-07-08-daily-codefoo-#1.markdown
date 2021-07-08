---
layout: post
title:  "Daily CodeFoo #1"
date:   2021-07-08 18:30:00 +0100
categories: jekyll update
---
One of the worst things about software nowadays are the unrelated coding puzzles candidates have to study for (either by grinding leetcode, reading cheat books, or being a new grad from a college with a good algo class). Saying this, I actually enjoy them! So I plan to try and set a streak of completing at least one each day and writing up about them on this blog. 

So, without further ado, time to start with puzzle 1! 

### Code Wars - Take a Ten Minute Walk - 6 Kyu

#### Summary 

You live in the city of Cartesia where all roads are laid out in a perfect grid. You arrived ten minutes too early to an appointment, so you decided to take the opportunity to go for a short walk. The city provides its citizens with a Walk Generating App on their phones -- everytime you press the button it sends you an array of one-letter strings representing directions to walk (eg. ['n', 's', 'w', 'e']). You always walk only a single block for each letter (direction) and you know it takes you one minute to traverse one city block, so create a function that will return true if the walk the app gives you will take you exactly ten minutes (you don't want to be early or late!) and will, of course, return you to your starting point. Return false otherwise.

Note: you will always receive a valid array containing a random assortment of direction letters ('n', 's', 'e', or 'w' only). It will never give you an empty array (that's not a walk, that's standing still!).

#### Formalization

Input is an array with at least one element from the set of {"n", "s", "e", "w"}.

A valid Input must have a length of 10.

A valid Input must end up at the same spot. 

#### Strategy

First we can eliminate all of trivial checks - any input greater than or less than 10 is incorrect.

After removing these we end up with a simple goal - can we end up at the starting spot after 10 moves? We need a way to track where we are and where we start. The first thing that comes to mind is using co-ordinates. If we start at 0 then we can add 1 for North and subtract 1 for South. However we need two dimensions and I can't be bothered passing around a tuple so I'll just increase the order of magnitude for East and West by 2. That means we have the following values for each move and if we end turn 10 with 0 then we're at the starting point. 

```
n =  1
s = -1
e =  100
w = -100
```

#### Implementation

This requires Four functions. First, a main function that takes an input and returns a boolean. Second, a function to validate the input. Third, a function that pattern matches the input to a value. Finally, a function to check the final result to see if it satisfies the original problem. The type signatures of these functions will be: 

{% highlight haskell %}
solve   :: [Char] -> Bool
valid   :: [Char] -> Bool
moveVal :: Char   -> Int
check   :: Int    -> Bool
{% endhighlight %}

Writing in psudo-Haskell, the `solve` function will look like this:
{% highlight haskell %}
solve input =
    if valid input
        then check result
        else False
    where
        result = sum $ map moveVal input
{% endhighlight %}

`valid` will just check the length as constraints already state it can only contain valid characters: 
{% highlight haskell %}
valid input =
    case input of
        length == 10 -> True
        _            -> False
{% endhighlight %}

We will need to pattern match on the move characters to return their respective int based on our decisions earlier - can't think of a better name than `moveVal` right now:
{% highlight haskell %}
moveVal c =
    case c of
        'n' -> 1
        's' -> (-1)
        'e' -> 100
        'w' -> -100
{% endhighlight %}

And finally `check`:
{% highlight haskell %}
check n =
    case n of
        0 -> True
        _ -> False
{% endhighlight %}

#### Summary

And there you have it. A few functions composed together and we have a solution. Representing two-dimensional positions as numbers in a single dimension is a quick and easy way to solve these styles of problems when you want to keep the data structures trivial, however only works within the guaranteed constraints a programming exercise offers! And, obviously, we could probably one-line this in Python with some dodgy nested list comprehension. 

But that's boring. 
