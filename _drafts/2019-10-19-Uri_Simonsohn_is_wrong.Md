---
layout: post
title: "Uri Simonsohn is wrong about hypothesis testing"
---

 A friend of mine[^1] recently drew my attention to a [blog post](http://datacolada.org/78a#identifier_1_4197) he thought I would find interesting. I'm told it's influential in the experimental social science world, for a couple of reasons. The primary reason for this is that the author - Uri Simonsohn - is concerned about a lack of methodological rigour in his field. Good on him for doing something about it! He's also definitely on the money with his argument in [this paper](https://scholar.google.com/citations?user=oY9xV3EAAAAJ#d=gs_md_cita-d&u=%2Fcitations%3Fview_op%3Dview_citation%26user%3DoY9xV3EAAAAJ%26citation_for_view%3DoY9xV3EAAAAJ%3ARGFaLdJalmkC), which roughly boils down to the argument that anything looks significant if you squint hard enough.
 
 So two cheers for Uri. The blog post of his that I read has some problems, however. Walking through the contents of it, here are some thoughts (comments in blockquotes are from the blog post, commentary is beneath):
 
 <script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML"></script>
 
### Correlation is not causation

The post starts off with this vignette:

>Would raising the minimum wage by $4 lead to greater unemployment? Milton, a Chicago economist, has a theory (supply and demand) that says so. Milton believes the causal effect is anywhere between 1% and 10%. After the minimum wage increase of $4, unemployment goes up 1%.  Milton feels bad about the unemployed but good about his theory.
>But then, Thomas, a Bayesian colleague, tells Milton to wipe that smile on his face, because his prediction was wrong. The Bayes factor for that 1% increase in unemployment 'supports the null' of no effect of wage on unemployment.

I don't actually have a problem with "Thomas"[^3] saying that. The argument here basically amounts to saying that if we observe evidence consistent with our hypothesis, then we should view it as the correct working theory of the world. I don't think it's as simple as that though - just because something you predicted happened, _doesn't mean it happened for the reason you suspect_. So what "Thomas" is saying in this example is that although the evidence you have may be consistent with your theory, that doesn't necessarily amount to something that could change your view of the world. Nowhere in this example is it made clear that the rise in unemployment is _specifically because_ of the increase in the minimum wage. Instead, "Milton" sees a correlation between these two measures and then ascribes the cause for fluctuations in the unemployment rate to the minimum wage change. So there's nothing wrong with "Thomas" telling a researcher to hold his horses, because there may be something else at play. The Bayes factor can reveal issues like this.[^4]

It's ironic that Professor Simonsohn has a problem with this exchange, given that the paper of his I linked above is about the prevalence of false positives being published in the experimental social science literature. Disregarding what "Thomas" is saying here could lead to precisely that happening!

### Partial understanding of the Bayes Factor

To explain how the Bayes factor works, Simonsohn poses this example:

> Bayes factors provide the results of a horse-race. They tell us how much more consistent the data are with an alternative hypothesis than with the null hypothesis. For example, if a pregnancy test is 10 times more likely to come up positive when pregnant than when not, then the Bayes factor is BF=10 for a positive result.

He's kind of onto something with the horse race analogy, but otherwise this isn't quite right. Let's start with a definition of the Bayes Factor. According to page 165 of _Machine Learning_ by Kevin P. Murphy, it can be written as follows:

$$ BF_{1,0} \triangleq \frac{p(D|M_{1})}{p(D|M_{0})} = \frac{p(D|M_{1})}{p(D|M_{0})} \Big/ \frac{p(M_{1})}{p(M_{0})}  $$

As the book rightly points out, it's very similar to a likelihood ratio, but with the unconditional model probability removed from the picture. Let's now return to the explanation provided by Professor Simonsohn. What are the models being compared in this example? The simple answer is, none. If he had a working hypothesis along the lines of "taking a pregnancy test makes you pregnant", or something similar, the Bayes factor could be used to quantify the strength of evidence in favour. What that example does is, again, provide a simple correlation. There's no outside theory actually being tested here, just a simple statement of facts derived from the data at hand. So it doesn't make sense to be talking about the Bayes factor in this puported example.

Expanding further on the Bayes factor, Simonsohn says:

> The BF for the pregnancy test is simple because the alternative hypothesis involves only one possibility: "being pregnant". But BFs are usually complicated because the alternative hypotheses they consider include many possibilities.

This seems obviously wrong: "being pregnant" is not a hypothesis, null or alternative. If instead "being pregnant" is not what he means to be a hypothesis, then what does he think is? One of the easiest ways to wind up with methodological problems is to not actually spell out in black and white the necessary background to a given claim. So the Bayes factor is discussed without mention of the hypotheses it is testing in the previous quote and in this one he rejects the Bayes factor as unnecessarily complicated without providing any evidence of the claim he makes to support it.

### Fundamental misunderstanding of hypothesis testing

To skip forward a little, Professor Simonsohn then provides this quote:

> If it is sufficiently closer to 0%, we "accept" the null.

This is, unfortunately, categorically incorrect. "Accepting the null" is not one of the outcomes of a hypothesis test under any circumstances and is the sort of thing first year math students are obliged to learn. Before anyone tries to get out of this one by saying it was in quotation marks, here are some other usages of it throughout the blog post:

> What would it take for you to conclude that the minimum wage does not increase unemployment? If you are like me, it would be something like this "if the estimated effect on unemployment were close enough to zero to rule out consequential effects, I will accept the null."

and 

> In sum.

> To use Bayes factors to test hypotheses: you need to be OK with the following two things:

> 1. Accepting the null when "the alternative" you consider, and reject, does not represent the theory of interest.

### Final thoughts

 The most fundamental of these is his use of the phrase "accept the null". This is flat out wrong and suggests he may not fully understand how hypothesis testing works. Particularly given that there's [another blog post by him](http://datacolada.org/42) that is in fact entitled "Accepting the Null" and is all about when it's acceptable to do so.[^2]
 
 [^1]: Who shall, of course, remain nameless
 [^2]: It's never acceptable to do so - I'll try and spell out why.
 [^3]: I'll give the author that he's choosing amusing names at least
 [^4]: More on this later
