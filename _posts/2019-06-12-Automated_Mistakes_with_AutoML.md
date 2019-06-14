---
layout: post
title: "How to automatically shoot yourself in the foot"
---

There are plenty of wonderful ways to screw up a perfectly good model. All of them share one common thread, which is that it's always possible to shoot yourself in the foot. Even funnier (from my point of view at least), is that the urge to shoot oneself in the foot increases as the complexity of the model you're working with does. In this post I'll discuss one simple way of achieving a precision shot by means of automating a parameter search.

To be clear, let's define shooting oneself in the foot:

> > "Shooting oneself in the foot consists of the ML practitioner evading complexity for the sake of mental, rather than computational, tractability. None of that stuff goes away because you ignore it lol." 
> 
> Stephen Hogg, 2019

This partly but not completely explains a fair bit of the interest in automating the search for an acceptable neural network architecture. Automating something like that isn't necessarily bad, but it can be if it's just being used to avoid thinking about how models work.

# The computer just does it for you

Here's a scenario that might lead you to want to partially automate things. You have a lot of text data and you need to discover topics in it. Obviously there are too many documents to read, so you use a model. One of the obvious candidates for doing this is Latent Dirichlet Allocation. 

Basically, LDA seeks to create a link between the words that are present in the collection (hereafter corpus), of documents you have and a number of latent (i.e. unobserved), topics. What this means in practice is that if you have an idea of how many topics there are in a corpus you can then get LDA to work out how they're defined.

The other piece of information LDA needs to work relates to the topics themselves. Specifically, how narrowly defined are they? Do you only need one or two words to establish the presence of a topic in a document, or more?

[Confused yet?](#confused-yet)

Ok, so you have two parameters to think about when searching for topics with LDA - one that governs how many topics and one that governs whether topics are narrowly or broadly defined. Now how do we tell which values are good?

With a model like LDA, typically you'd evaluate the _per word perplexity_. That's a mouthful, so let's start with the last word.

Imagine you're playing cards with someone. Normal deck of 52 as is common in the West, nothing too funny going on. Your opponent draws a card unseen to you. What could it be?

If you don't know anything at all and have to make a wild guess, then there are 52 potential cards you could guess from. You have terrible odds of being right. In this case, your perplexity is 52 - the number of states you need to choose from.

If, on the other hand, you know what cards are in your own hand or have seen others previously, then you can eliminate them as possibilities. If you can eliminate, say 6 cards, then that leaves 46 possible cards your opponent may have drawn. So perplexity is now 46 and you're still guessing, but with a bit more clarity.

Going back to LDA (this is the _per word_ part of _per word perplexity_), what gets measured is how strongly each word in the vocabulary of your corpus is associated to any one topic. If you have no idea which topic a word relates to, then perplexity will be equal to the number of topics. Equally, if a given word clearly relates to only one topic then perplexity drops to one. You'll get a range of outcomes for the words you're working with, so it just gets averaged and called _per word perplexity_.

# This all seems fine

So we have a couple of levers and a way of telling whether words are getting more or less tightly associated with topics. More is better, generally. So now we can rig up something to try a few different combinations of values for the number of topics and how narrowly defined they are, check the perplexity and pick whatever has the lowest score.

And that's where things go wrong. Back when I used to work in a call centre, people used to constantly say that what gets measured, gets managed. So if all you worry about is the uniqueness of the relationship between words and topics, that's what you'll get!

It turns out that if you try to optimise both the number of topics and their narrowness at the same time, you wind up in either of two trivial cases.

1) One MASSIVE topic, strongly connected to every single word so that every document has the same primary topic

2) One topic per word, so that you haven't really clustered anything at all and are really just calculating term frequency without realising

Both of these outcomes are rubbish, obviously. It's worth noting that they could also appear by stealth: a configuration with 30 topics but all the words are associated to only one of them could happen, for example. You'd then inadvertently pick it as the optimal configuration and think everything is hunky dory because the parameters that led to that scenario don't seem untoward.

# Time to eat your vegetables

The warning that this was going to fail happened in the word "generally", in the previous paragraph. How precisely did this stuff up, though?

Firstly, doing things this way basically consisted of trying to abstract away thinking about how the model works. Secondly, the phrase _what gets measured, gets managed_ really matters here. When automatically optimising something, first take a second to think. If you managed to get that score all the way down (or up), would that actually be the outcome you wanted? A lot of the time the answer is yes, but it's the times when the answer is really no that will get you. Just a little bit of thinking saves a lot of work.

Another thing to think about is how ambitious you get about automatically optimising stuff. If you decided to have an opinion about the narrowness of topics, then your task would simply be a matter of employing something like the [Elbow method](https://en.wikipedia.org/wiki/Elbow_method_(clustering)) to make a choice about the right number of topics. This is much less fraught because you now have some guardrails for the process. The same in reverse applies to fixing the number of topics and searching over the narrowness of their definition.

Finally, note that I have not recommended making the metric you optimise more complicated to account for some of these quirks. Down that road lies madness, but go ahead if you really want. Good luck with that haha.
