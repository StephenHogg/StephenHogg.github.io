---
layout: post
title: "Another way to look at risk versus reward in binary classification"
---
<script type="text/javascript" async  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML"></script>

Models in production are software, so why don't we think about how badly they might perform? That is, when we put a model into production we tend to assume that test accuracy/F1/AUC is fixed and won't change, even though we generally know that's not true. So why don't we try and make a guess at how much lower our performance might reasonably turn out to be? In this post, I'll look at one way of doing this with a binary classifier. If you don't want to worry about the details, just [skip to the final section](#the-bigger-picture)

Of course, the worst case is that your model gets absolutely everything wrong. That's (hopefully) way off in the tails of your likely outcomes and not the point of this exercise, though. What I'm aiming for here is a way of looking at how much a model might underperform plausibly.

Another thing to quickly draw your attention to is how one might traditionally analyse the risk of a classifier. This can be summarised as identifying a cost associated with a false positive and multiplying that by the number of false positives in your test set, followed by the same for false negatives. This is different, because it takes model performance as fixed rather than asking by how much it might vary.

# Gotta risk it to get the biscuit

Before you do anything, you need a decent baseline to compare to. What might we do in the absence of a model? There are plenty of options including the performance of coin-flipping, constant-valued prediction and others up to and including a simple model that you're already happy with.[^1]

For the purpose of this discussion, let's just say that your baseline model is constant-valued and just spits out whatever the majority class is irrespective of the data.[^2] So what does this mean for performance?

Imagine you've got a dataset where 90% of the labels are negative and the remaining 10% are positive. Obviously, the constant-valued classifier gives you 90% accuracy. So if you do any worse than that on a model you've built, it's fair to claim that you've wasted your time. 

This is where things get interesting. We can be pretty confident about that 90% accuracy figure - the model is quite simple and as long as data remains in those proportions in the wild it should hold up reasonably well.[^3] The more complex your model is though, the more open you are to things getting funky.[^4] So it's reasonable to ask yourself: 

> "Given the extra performance above a baseline model I see, how much risk do I take in exchange?"

...because after all, there ain't no such thing as a free lunch!

# Down on the upside[^5]

Working out the outperformance of a model compared to a baseline classifier in accuracy terms is easy. All you do is subtract the baseline accuracy you've got from your model's reported test accuracy. If that comes out negative, stop reading: you have bigger problems.

# This is where it gets confusing

Now how much risk are you taking on to get the outperformance you see? One way of looking at this involves [model perplexity (brief explanation you should read here)](https://breakitdownto.earth/2019/06/12/Automated_Mistakes_with_AutoML.html#confused-yet). The question is, how to arrive at that measure for a binary classifier. The good news is that it's not hard. Binary cross-entropy - perhaps the most commonly used loss function for binary classifiers - can be converted into a perplexity score easily. 

Wikipedia helpfully informs us that[^6]:

> The perplexity of a discrete probability distribution p is defined as:
>
> $$2^{H(p)}=2^{-\sum _{x=1} p(x)\log _{2}p(x)}$$

Don't worry about why there's a 2 used there - what this tells us is that you can convert entropy (i.e. binary cross-entropy) into perplexity by just exponentiating with the same base as you used in your entropy calculation. So if you used the natural log when calculating cross-entropy, all you need to do is:

$$ e^{H(p)} $$

and you've got a perplexity score. We can turn a perplexity into an estimated accuracy score by seeing that the probability of making an accurate prediction in the worst case is equal to a random guess from the possible states (after your model has excluded obviously incorrect ones). So this means that you can get a plausible lower-bound accuracy for your classifier as follows:

$$ ACC_{lowerbound} = \frac{1}{e^{loss}} $$

# The bigger picture

So we now have three numbers to work with:

1. The accuracy as reported on our test set
2. The accuracy that would be achieved by a baseline model
3. The estimate we have of how badly our model might plausibly perform in the wild

Now it's just a matter of judgement really - given how well your model appears to perform, is the risk on the downside worth it?

Here's a scenario. You have a model with the following results:

1. Reported test set accuracy of 93% (implying 3% of upside on a baseline classifier)
2. A baseline accuracy of 90%
3. An estimate for accuracy in the worst case arrived at using the previous section of 75% (implying quite a lot of downside)

It looks like the model takes on quite a bit of risk for the upside it appears to be capturing, so you may think twice about putting this model into production. Equally, it's not hard to think about another situation where the worst case accuracy indicated by transforming cross-entropy is not far below a random baseline at all. 

None of this is necessarily all that revolutionary, but what it does do (and what's important here), is let you think explicitly about how much trouble a model might cause you in production before you actually go live with it. Finally, it's also worth knowing that you can do this with other metrics with a certain amount of jiggery pokery. 

Hooray!


[^1]: Big caveat with this last one. If you're not respecting the word "simple", it probably shouldn't be a baseline. The idea is to work out how much better of you are compared to no model.
[^2]: You could use something else, though.
[^3]: Sure, it might not. 
[^4]: This is basically how adversarial attacks on ML models have become a thing. The more complicated models get, the more room there is for this. But this is an aside.
[^5]: Yup. Soundgarden jokes.
[^6]: https://en.wikipedia.org/wiki/Perplexity