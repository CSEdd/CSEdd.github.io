---
layout: post
title:  "Editing records with lenses"
date:   2021-07-08 09:02:02 +0100
categories: jekyll update
---
I'm currently working on a [Dominion](https://github.com/CSEdd/domin8) simulator in Haskell which requires a few constantly changing records to accurately represent. While I first looked at using functions that returns an updated record, I realised this would get complex as the records became more nested and complicate rather simple logic. 

{% highlight haskell %}
data Card = Card {
  name     = CardName,
  value    = CardValue, 
  cardType = CardType
}

data Deck = Deck {
  cards = [Card]
}

data Hand = Hand {
  cards = [Card]
}

drawCard    :: Deck -> Hand -> Hand
discardHand :: Hand -> Hand
discardCard :: Hand -> Hand
-- etc...
{% endhighlight %}

What I wanted to do is just update a records field in the 'cleanest' way possible with minimal line noise. That's when I started looking at Lens, a Haskell library that lets you have CRUD-like access to deeply nested record types. After battling the usual Haskell jargon for an afternoon I got a few of the simpler lenses working and thought I'd store them here for the next time I need them. 

> The combinators in Control.Lens provide a highly generic toolbox for composing families of getters, folds, isomorphisms, traversals, setters and lenses and their indexed variants.  - Huh?

First we declare our imports, language extensions, and create a new record type. 

{% highlight haskell %}
{-# LANGUAGE TemplateHaskell #-}

import Control.Lens

data Person = Person {
  _name = String,
  _age  = Int
}
makeLenses ''Person
{% endhighlight %}

There's a little magic going on here. First we mark a record to be lens'd by adding `makeLenses ''<recordName>`. We then mark each field in that record to be lens'd by prepending them with underscores. After this we can get, set, and generall update complex records in a much simpler way (albeit with some pretty interesting syntax choices).

{% highlight haskell %}
-- View
person ^. name

-- Set
person $ name .~ "CSEdd"

-- Modify
person $ name %~ "Edd"
{% endhighlight %}

You can also use Lenses on other datatypes too. For example if you wanted to get the third characther of "Lenses" you could write `"Lenses" ^? ix 3`. Told you the syntax was interesting right? 

You can read more about Lens [here](https://hackage.haskell.org/package/lens-5.0.1/docs/Control-Lens-Fold.html) or Edward Kmetts FAQ [here](https://github.com/ekmett/lens/wiki/FAQ).