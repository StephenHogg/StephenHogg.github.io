---
layout: post
title: "Topic Generation, Quickly"
image: "/assets/img/Brain.png"
---

Some of the tricks outlined in earlier posts add up to something that I've found useful. Specifically, they form a way of generating topic labels and from there models.
In this post I'll attempt to explain how it works.

# The Set-up

Imagine you've got a large amount of free text data, with no labels for the documents. You want to be able to classify them, so what can you do? 
Here are your options:

<img src="/assets/img/Brain.png" width="400" height="600" />

These options are ordered according to the amount of labour involved, with manual annotation the most and blogging the least.

# Manually Annotating Everything 

Urgh. At least get Mechanical Turk to do it or something. And while you're at it, [it's not hard to pay your workers fairly](https://fairwork.stanford.edu/). This is obviously the most labourious choice, which causes a few problems. Firstly, it's going to take you ages to actually get to the point where you know if this is working or not. Secondly, a lot of examples won't really be useful because they're a long way from your (hoped-for) decision boundary. You'll probably also run the risk of procrastinating, thereby lengthening and already unnecessarily long task. 

There's another sleeper problem here as well. How do you know what the topics are before you start labelling? This is a killer. It's easy to get partway through labelling a large number of documents only to realise your taxonomy is wrong, necessitating a restart. 

# Semi-Supervised Learning

This is a bit better. Instead of labelling everything, pick some stuff that represents the 
