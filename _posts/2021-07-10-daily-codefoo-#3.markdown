---
layout: post
title:  "Daily CodeFoo #3"
date:   2021-07-10 09:30:00 +0100
categories: jekyll update
---

So the choice of CodeFoo challenge is random by selecting 'train' on CodeWars and todays was a little short. I guess they will just as likely be difficult in the future so I'll go ahead and post it rather than find another. 

#### Problem

Return the number (count) of vowels in the given string.

We will consider a, e, i, o, u as vowels for this Kata (but not y).

The input string will only consist of lower case letters and/or spaces.

#### Formalization

```
Input = [String]
Length = >= 0
{a, e, i, o, u} = 1; {_} = 0
```

#### Implementation

{% highlight haskell %}
isVowel :: Char -> Int
isVowel c = 
  case c of
    'a' -> 1
    'e' -> 1
    'i' -> 1
    'o' -> 1
    'u' -> 1
    _   -> 0

getCount :: String -> Int
getCount s = sum $ map isVowel s
{% endhighlight %}

#### Summary

I'm currently working on an interview tech test of implementing a calculator byte code interpreter which is taking a bit of time (I took compilers class once in Java on a Java-ish language) so I guess I got lucky with having this one today. As long as you remember that `[Char] == String` then pattern matching on characters is nice and easy. 