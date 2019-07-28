---
layout: post
title: "A Hack to Avoid Labelling Topic Classification Data"
image: "/assets/img/Brain.png"
---

Some of the tricks outlined in earlier posts add up to something that I've found useful. Specifically, they form a way of generating topic labels and from there classification models.
In this post I'll attempt to explain how it works.

# The Set-up

Imagine you've got a large amount of free text data, with no labels for the documents. You want to be able to classify them, so what can you do? 
Here are your options:

<img src="/assets/img/Brain.png" width="400" height="600" />

These options are ordered according to the amount of labour involved, with manual annotation the most and blogging the least.

# Manually Annotating Everything 

Urgh. At least get Mechanical Turk to do it or something. And while you're at it, [it's not hard to pay your workers fairly](https://fairwork.stanford.edu/). This is obviously the most labourious choice, which causes a few problems. Firstly, it's going to take you ages to actually get to the point where you know if this is working or not. Secondly, a lot of examples won't really be useful because they're a long way from your (hoped-for) decision boundary and therefore don't really play much of a role in training. You'll probably also run the risk of procrastinating, thereby lengthening an already unnecessarily long task. 

There's another sleeper problem here, as well. How do you know what the topics are before you start labelling? This is a killer. It's easy to get partway through labelling a large number of documents only to realise your taxonomy is wrong, necessitating a restart. 

# Semi-Supervised Learning

This is a bit better. Instead of labelling everything, pick some stuff that represents a few topics you're interested in and try to capture the latent structure of all the unlabelled data when you build a model. This involves potentially a lot less manual labour than the previous option, but there's still a fair bit of work to do. There are other problems as well. 

As with full manual annotation, you're still stuck with the task of working out what is actually _in_ your data before manually labelling anything. Which is still the same chicken-and-egg problem. Another problem lurks in the question: how much is actually enough?
Finally, semi-supervised learning is a bit tricky because of the weird likelihood function among other things. That said, on this last point [shortcuts do exist](https://breakitdownto.earth/2019/07/12/Semi-Supervised_Learning_Trick.html).

If you're feeling really advanced, you might try some sort of active learning after you've labelled some examples. In my experience this doesn't work out as planned, because unless you've labelled heaps of data everything still looks novel to a classifier. You wind up just labelling all the examples you send to active learning. So that's not really a shortcut either. Still, at least with this option you don't necessarily do _as much_ manual labelling.

# Multi-part Modelling Weirdness

Given that we need some idea of topics before we start labelling them, how can we achieve this? There are plenty of unsupervised tools out there, but let's look at LDA ([Latent Dirichlet Allocation](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation), not [Linear Discriminant Analysis](https://en.wikipedia.org/wiki/Linear_discriminant_analysis)) for a second.

<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML"></script>

When looking for topics in LDA, you have access to a parameter usually denoted $$\alpha$$. This governs how broadly-defined the topics you're looking for are. What you might consider doing is setting that to be something narrow (i.e. 0.8-0.9) and then using that to arrange your documents into small, similar clumps.

So far so good. Now for each topic you can just inspect a few of the most strongly-associated documents and decide what it's about. This is still manual labour in a way, but not nearly as onerous and you get a lot more bang for your buck. For each document in, say, the top 10% by score of a given topic, label it with that topic. With an idea of what your topics are about you can put a few of them together in a class, giving rise to large amount of coherently labelled data with comparatively little work.

Now what you're left with is a bunch of documents where you can be confident of their class membership and a much larger body that may or may not be members of the classes you've created. Which is basically the definition of PU-learning, so [the trick I alluded to earlier](https://breakitdownto.earth/2019/07/12/Semi-Supervised_Learning_Trick.html) applies here.

Long story short, if you use LDA to identify groupings of documents, you can turn them into classification labels easily. Then it's just a matter of training your model in the right way. Simple!

# Writing a Blog About It

Obviously the easiest bit. Ta da!


