---
layout: post
title:  "Daily CodeFoo #2"
date:   2021-07-09 10:30:00 +0100
categories: jekyll update
---

### Code Wars - Who likes it? - 6 Kyu

#### Problem

You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement a function likes :: [String] -> String, which must take in input array, containing the names of people who like an item. It must return the display text as shown in the examples:

{% highlight haskell %}
likes [] -- must be "no one likes this"
likes ["Peter"] -- must be "Peter likes this"
likes ["Jacob", "Alex"] -- must be "Jacob and Alex like this"
likes ["Max", "John", "Mark"] -- must be "Max, John and Mark like this"
likes ["Alex", "Jacob", "Mark", "Max"] -- must be "Alex, Jacob and 2 others like this"
{% endhighlight %}

#### Formalization

```
Input = [String]
Len Input >= 0
Outputs = 
    | "no one likes this"
    | "{name1} likes this"
    | "{name1} and {name2} like this"
    | "{name1}, {name2} and {name3} like this"
    | "{name1}, {name2} and {n-2} others like this"
```

#### Implementation

So the formalization is actually _very_ similar to Haskell code and we can essentially do a one-to-one copy albeit with some string formatting. 

{% highlight haskell %}
likes :: [String] -> String
likes people
  | length people == 0 = "no one likes this"
  | length people == 1 = people !! 0 ++ " likes this"
  | length people == 2 = people !! 0 ++ " and " ++ people !! 1 ++ " like this"
  | length people == 3 = people !! 0 ++ ", " ++ people !! 1 ++ " and " ++ people !! 2 ++ " like this"
  | otherwise          = people !! 0 ++ ", " ++ people !! 1 ++ " and " ++ (show $ length people - 2) ++ " others like this"
{% endhighlight %}

It would be nice to take the string manipulation out into its own function. However, because CodeWars doesn't like imports, all I could do is move the same code out into another function which seems pointless. Ideally we could use `printf` from `Text.Format` to generalize it a little more. 

#### Summary

It's nice to see how semi-formalizing a problem and its implementation can be so similar. This is a pretty simple problem but I still think it shows some of the perks of pattern matching in a language. 