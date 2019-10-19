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

I don't actually have a problem with "Thomas"[^3] saying that. The argument here basically amounts to saying that if we observe evidence consistent with our hypothesis, then we should view it as the correct working theory of the world. I don't think it's as simple as that though - just because something you predicted happened, _doesn't mean it happened for the reason you suspect_. So what "Thomas" is saying in this example is that although the evidence you have may be consistent with your theory, that doesn't necessarily amount to something that could change your view of the world. Nowhere in this example is it made clear that the rise in unemployment is _specifically because_ of the increase in the minimum wage. Instead, "Milton" sees a correlation between these two measures and then ascribes the cause for fluctuations in the unemployment rate to the minimum wage change. So there's nothing wrong with "Thomas" telling a researcher to hold his horses, because there may be something else at play. 

It's ironic that Professor Simonsohn sees this exchange as undesirable, given that the paper of his I linked above is about the prevalence of false positives being published in the experimental social science literature. Disregarding what "Thomas" is saying here could lead to precisely that happening!

### Partial understanding of the Bayes Factor

To explain how the Bayes factor works, Simonsohn poses this example:

> Bayes factors provide the results of a horse-race. They tell us how much more consistent the data are with an alternative hypothesis than with the null hypothesis. For example, if a pregnancy test is 10 times more likely to come up positive when pregnant than when not, then the Bayes factor is BF=10 for a positive result.

He's kind of onto something with the horse race analogy, but otherwise this isn't quite right. Let's start with a definition of the Bayes Factor. According to page 165 of _Machine Learning_ by Kevin P. Murphy, it can be written as follows:

$$ BF_{1,0} \triangleq \frac{p(D|M_{1})}{p(D|M_{0})} = \frac{p(M_{1}|D)}{p(M_{0}|D)} \Big/ \frac{p(M_{0})}{p(M_{1})}  $$

As the book rightly points out, it's very similar to a likelihood ratio, but with the unconditional model probability removed from the picture. Let's now return to the explanation provided by Professor Simonsohn. What are the models being compared in this example? The simple answer is, none. If he had a working hypothesis along the lines of "taking a pregnancy test makes you pregnant", or something similar, the Bayes factor could be used to quantify the strength of evidence in favour _or against_. What the above example does is, again, provide a simple correlation. There's no outside theory actually being tested here, just a simple statement of facts derived from the data at hand. So it doesn't make sense to be talking about the Bayes factor in this puported example.

Expanding further on the Bayes factor, Simonsohn says:

> The BF for the pregnancy test is simple because the alternative hypothesis involves only one possibility: "being pregnant". But BFs are usually complicated because the alternative hypotheses they consider include many possibilities.

This seems obviously wrong: "being pregnant" is not a hypothesis, null or alternative. If instead "being pregnant" is not what he means to be a hypothesis, then what does he think is? One of the easiest ways to wind up with methodological problems is to not actually spell out in black and white the necessary background to a given claim. So the Bayes factor is inaccurately defined without mention of the hypotheses it is testing in the previous quote and in this one he rejects the Bayes factor as unnecessarily complicated without providing any evidence to support that claim.

### Fundamental misunderstanding of hypothesis testing

To skip forward a little, Professor Simonsohn then provides this quote:

> If it is sufficiently closer to 0%, we "accept" the null.

This is, unfortunately, categorically incorrect. "Accepting the null" is not one of the outcomes of a classical null hypothesis test under any circumstances and is the sort of thing first year math students are obliged to learn. Before anyone tries to get out of this one by saying it was in quotation marks, here are some other usages of it throughout the blog post:

> What would it take for you to conclude that the minimum wage does not increase unemployment? If you are like me, it would be something like this "if the estimated effect on unemployment were close enough to zero to rule out consequential effects, I will accept the null."

and 

> In sum.
>
> To use Bayes factors to test hypotheses: you need to be OK with the following two things:
>
> 1\. Accepting the null when "the alternative" you consider, and reject, does not represent the theory of interest.

note that one doesn't reject an alternative hypothesis either, only the null. And in the footnotes:

> 5. The default "the alternative", e.g., the one used by the BayesFactors R package, involves a distribution centered at zero, and where every real number is possible, thus any observed value is consistent with the alternative defined this way, and therefore, every time you accept the null, you have observed a value that 'the alternative' gives some probability to being true.  But this does not need to be the case. The alternative could be just one value (see previous footnote). Also, the null could be defined around zero not exactly at zero so here some observed values would belong to the null and not to the alternative. But, even in this latter case, it will still quite often be the case that a value predicted by the alternative and not by the null will lead the Bayes factor to support the null

and [another entire blog post](http://datacolada.org/42) (click for link) that is in fact entitled "Accepting the Null" and is all about when it's acceptable to do so.[^2]

This wouldn't be as big of a deal if he were talking about a comparison of two theories without either having a privileged "null" position in the test.[^6] But he's talking (repeatedly), about a "null" hypothesis so it's hard not to conclude that he's thinking about all of this in terms of the classical null hypothesis significance test.

How does a null hypothesis significance test work, then? It's kind of complex yet straightforward. The overarching idea is that you're never actually 100% certain of anything, nor that one should change their mind without conclusive evidence suggesting that one do so.[^5] You're not supposed to ever reach a point whereby you're absolutely certain of what's going on and therefore never finally "accept" any theory. This is why the options available to the researcher in a classical null hypothesis test are "reject the null hypothesis" and "do not reject the null hypothesis", _and nothing else_. So it's kind of worrying that Professor Simonsohn is thinking (perhaps subconsciously) about hypothesis testing as a way of arriving at definitive proof instead of just as a way of gradually improving one's understanding of the world.

I should note, this is not to say that the null hypothesis test framework as it stands is perfect. The point of the above is only that Professor Simonsohn is not operating correctly within the framework he's chosen to adopt for the purposes of talking about the Bayes factor.

### False positives

Cast your mind back to the very first example I talked about, and the risk of a false positive arising in a situation like that. Now look at this remark:

>In sum.
>
>...
>
>2\. Rejecting a theory after observing an outcome that the theory predicts.

So the point being made here, is that if you see evidence consistent with your hypothesis, it would be wrong to do anything other than treat your hypothesis as proven. This is absolutely a recipe for false positives, for the correlation-versus-causation reasons discussed above among other things. Further, you don't need to use a Bayes factor in your investigations to make this mistake - all you need to do is have a confirmation bias. So this, and the other, recommendation that Professor Simonsohn makes about the use of the Bayes factor should be disregarded, in my view. There are problems with every framework, including the Bayesian one, but those problems aren't the ones that Professor Simonsohn talks about in his blog post.

### Final thoughts

There's more to talk about here, but let's wrap it up.

 After talking with my nameless friend about all of this, he posed one simple question to me: seeing as he's been going since 2011, why hasn't he been called out for this stuff yet? The obvious answer seems like the simplest one to me - Uri Simonsohn is right. The audience he's talking to doesn't have a very good understanding of the fundamentals of scientific investigation. This implies that mistakes he makes are less likely to be caught. Therefore, it seems advisable that he take greater care with his own advocacy for the sake of what is absolutely an admirable change within his chosen field of research.
 
 If you'd like some more reading about the Bayes factor that sheds greater light on the way hypothesis testing and Bayesian statistics work together, I heartily recommend [this presentation](https://modeling.uconn.edu/wp-content/uploads/sites/1188/2016/05/Bayes-Factor-Null-Hypothesis-Tests-are-still-Null-Hypothesis-Tests.pdf) from Matt Williams.
 
 Finally, I've emailed the link to this to Professor Simonsohn and his co-authors seeking comment. It's fair that they have a right of reply, so if they choose to do so I will add it to this post.
 
 It's a funny old world!
 
 [^1]: Who shall, of course, remain nameless
 [^2]: It's never acceptable to do so - I'll try and spell out why.
 [^3]: I'll give the author that he's choosing amusing names at least
 [^5]: What constitutes conclusive evidence is of course another matter
 [^6]: It still would be, though
