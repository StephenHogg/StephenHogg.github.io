---
layout: post
title: "How to automatically shoot yourself in the foot"
---

There are plenty of wonderful ways to screw up a perfectly good model. All of them share one common thread, which is that it's always possible to shoot yourself in the foot. Even funnier (from my point of view at least), is that the urge to shoot oneself in the foot increases as the complexity of the model you're working with does. In this post I'll discuss one simple way of achieving a precision shot on one's foot by means of automating a parameter search.

To be clear, let's define shooting oneself in the foot:

> 
> > "Shooting oneself in the foot consists of the ML practitioner evading complexity for the sake of mental, rather than computational, tractability." 
> 
> Stephen Hogg, 2019

This partly (but not completely), explains a fair bit of the interest in automating the search for an acceptable neural network architecture. That isn't necessarily bad, but it can be if it's just being used to avoid thinking about how models work.

# The computer just does it for you

Here's a scenario that might lead you to want to partially automate things. You have a lot of text data and you need to discover topics in it. Obviously there are too many documents to read, so you use a model. One of the obvious candidates for doing this is Latent Dirichlet Allocation. 

Ok so how does that work? 

Basically, LDA seeks to create a link between the words that are present in the collection (hereafter corpus), of documents you have and a number of latent (i.e. unobserved), topics. What this means in practice is that if you have an idea of how many topics there are in a corpus you can then get LDA to work out how they're defined.