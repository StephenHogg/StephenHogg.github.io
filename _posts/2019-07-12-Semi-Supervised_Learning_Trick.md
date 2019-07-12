---
layout: post
title: "How to avoid doing semi-supervised learning"
---

It's easy to find yourself solving a problem with labels for only _some_ of your data. This creates a quandary - what to do about the rest of your unlabelled data? There are a few possible answers:

* Ignore it and just work with what you have
* Try to include it, but:
    * Do so without making any guess about what the true label is
    * Try to infer the missing labels first

As you'd guess, all of the above are a nightmare. If you ignore your unlabelled data, you're setting up an obvious bias problem. If you try to include unlabelled data as-is the math starts getting complicated. And trying to infer the missing labels first can create noise if you're not careful. So how can we get out of all of this? This post is about one possible answer.

# The Set-Up

Incorporating unlabelled data in a model falls under the heading of "semi-supervised" learning. One particular example of this is "positive-unlabelled" learning. This consists of having labels for some positive examples and many unlabelled examples. This is a pretty common scenario and one I've found myself in before.

Semi-supervised learning is useful but complex, so it's better to achieve the same thing by simpler means. If you wanted to go down that path, you'd have to code up a fairly complicated likelihood. Instead, it turns out that you can have basically the same gradient without that. Thanks to [Paul Mineiro pointing this paper out](http://www.machinedlearnings.com/2012/03/pu-learning-and-auc.html), we know that the AUC of a full-labelled model is proportionate to one with only positive labels available. As he says, this means you can just treat unlabelled examples as members of the negative class. Once you've done that, all you need to do is optimise AUC.

# Optimising AUC

Optimising AUC is tricky because there's no gradient to work with. The simplest definition of it boils down to repeated random sampling from the positive and negative classes. The obvious thing to do is employ an age-old trick, summed up as follows:

> "When you don't know how to solve something, try to solve something else"

In AUC terms, this means adopting a pairwise loss or ranking-based metric. Parwise loss metrics generally mimic the kind of thing that AUC is trying to characterise. If you're lucky enough to be working with something like Tensorflow, then these are readily available. If you go down this path, then it's a simple matter of just altering regularisation parameters and learning rates to taste. 

You might also instead use whatever loss function you were planning to use but just keep track of AUC anyway. One final thought with regards to this is that any metric you can get from the 2x2 confusion matrix can be optimised by altering the class weights. AUC is based on the true positive and false positive rates, so it falls into this category.
