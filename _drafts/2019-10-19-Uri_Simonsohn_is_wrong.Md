---
layout: post
title: "Uri Simonsohn is wrong about hypothesis testing"
---

 A friend of mine[^1] recently drew my attention to a [blog post](http://datacolada.org/78a#identifier_1_4197) he thought I would find interesting. I'm told it's influential in the experimental social science world, for a couple of reasons. The primary reason for this is that the author - Uri Simonsohn - is concerned about a lack of methodological rigour in his field. Good on him for doing something about it! He's also definitely on the money with his argument in [this paper](https://scholar.google.com/citations?user=oY9xV3EAAAAJ#d=gs_md_cita-d&u=%2Fcitations%3Fview_op%3Dview_citation%26user%3DoY9xV3EAAAAJ%26citation_for_view%3DoY9xV3EAAAAJ%3ARGFaLdJalmkC), which roughly boils down to the argument that anything looks significant if you squint hard enough.
 
 So two cheers for Uri. The blog post of his that I read has some problems, however. Walking through the contents of it, here are some thoughts (comments in blockquotes are from the blog post, commentary is beneath):
 
### Correlation is not causation

The post starts off with this vignette:

>Would raising the minimum wage by $4 lead to greater unemployment? Milton, a Chicago economist, has a theory (supply and demand) that says so. Milton believes the causal effect is anywhere between 1% and 10%. After the minimum wage increase of $4, unemployment goes up 1%.  Milton feels bad about the unemployed but good about his theory.
>But then, Thomas, a Bayesian colleague, tells Milton to wipe that smile on his face, because his prediction was wrong. The Bayes factor for that 1% increase in unemployment 'supports the null' of no effect of wage on unemployment.

I don't actually have a problem with "Thomas"[^3] saying that. The argument here basically amounts to saying that if we observe evidence consistent with our hypothesis, then we should view it as the correct working theory of the world. I don't think it's as simple as that though - just because something you predicted happened, _doesn't mean it happened for the reason you suspect_. So what "Thomas" is saying in this example is that although the evidence you have may be consistent with your theory, that doesn't necessarily amount to something that could change your view of the world. Nowhere in this example is it made clear that the rise in unemployment is _specifically because_ of the increase in the minimum wage. Instead, "Milton" sees a correlation between these two measures and then ascribes the cause for fluctuations in the unemployment rate to the minimum wage change. So there's nothing wrong with "Thomas" telling a researcher to hold his horses, because there may be something else at play. The Bayes factor can reveal issues like this.[^4]

It's ironic that Dr Simonsohn has a problem with this exchange, given that the paper of his I linked above is about the prevalence of false positives being published in the experimental social science literature. Disregarding what "Thomas" is saying here could lead to precisely that happening!

### Partial understanding of the Bayes Factor

To explain how the Bayes factor works, Simonsohn poses this example:

> Bayes factors provide the results of a horse-race. They tell us how much more consistent the data are with an alternative hypothesis than with the null hypothesis. For example, if a pregnancy test is 10 times more likely to come up positive when pregnant than when not, then the Bayes factor is BF=10 for a positive result.

This isn't quite right. Let's start with a definition of the Bayes Factor. According to page 165 of _Machine Learning_ by Kevin Murphy, it can be written as follows:



### Final thoughts

 The most fundamental of these is his use of the phrase "accept the null". This is flat out wrong and suggests he may not fully understand how hypothesis testing works. Particularly given that there's [another blog post by him](http://datacolada.org/42) that is in fact entitled "Accepting the Null" and is all about when it's acceptable to do so.[^2]
 
 [^1]: Who shall, of course, remain nameless
 [^2]: It's never acceptable to do so - I'll try and spell out why.
 [^3]: I'll give the author that he's choosing amusing names at least
 [^4]: More on this later
