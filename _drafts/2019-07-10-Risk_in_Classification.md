---
layout: post
title: "Another way to look at risk versus reward in binary classification"
---
<script type="text/javascript" async  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML"></script>

Models in production are software, so why don’t we think about how badly they might perform? When we put a model into production we tend to take test accuracy/F1/AUC as given, even though we generally know that’s not true. So why don’t we try and make a guess at how much lower our performance might turn out to be? In this post, I’ll look at one way of doing this with a binary classifier. If you don’t want to worry about the details, [skip to the final section](#the-bigger-picture)

Of course, the worst case is that your model gets everything wrong. That’s way off in the tails of your likely outcomes and not the point of this exercise, though. What I’m aiming for here is a way of looking at how much a model might underperform in reality.

# Gotta risk it to get the biscuit

Before you do anything, you need a decent baseline to compare to. What might we do in the absence of a model? You could flip a coin. Or you could always predict the commonest class. You could even use another much simpler model.[^1]

For now, let’s say that your baseline model is constant-valued. The model predicts all data are from the majority class.[^2] So what does this mean for performance?

Imagine you’ve got a dataset where 90% of the labels are negative and the remaining 10% are positive. The constant-valued classifier gives you 90% accuracy. So if you do any worse than that on a model you’ve built, it’s fair to claim that you’ve wasted your time.

This is where things get interesting. We can be pretty confident about that 90% accuracy figure, because the model is simple. The more complex your model is though, the more open you are to things getting funky.[^4] 

So it's reasonable to ask yourself: 

> "Given the extra performance above a baseline model I see, how much risk do I take in exchange?"

...because after all, there ain't no such thing as a free lunch!

# Down on the upside[^5]

It's easy to work out how much upside you're capturing relative to a baseline. All you do is subtract the baseline accuracy you’ve got from your model’s reported test accuracy. If that comes out negative, stop reading: you have bigger problems.

# This is where it gets confusing

Now how much risk are you taking on to get the outperformance you see? One way of looking at this involves [model perplexity (brief explanation you should read here)](https://breakitdownto.earth/2019/06/12/Automated_Mistakes_with_AutoML.html#confused-yet). The question is, how to arrive at that measure for a binary classifier. The good news is that it’s not hard. It's easy to turn binary cross-entropy into a perplexity score.

Wikipedia informs us that[^6]:

> The perplexity of a discrete probability distribution p is defined as:
>
> $$2^{H(p)}=2^{-\sum _{x=1} p(x)\log _{2}p(x)}$$

The bit on the left side is the important thing here. Perplexity is equal to a base raised to the power of entropy. The base needs to be the same as the one used calculating entropy. So if you used the natural log when calculating cross-entropy, all you need to do is:

$$ perplexity = e^{entropy} $$

and you’ve got a perplexity score. Perplexity can become an estimated accuracy score, too. If you know that only a couple of outcomes are plausible, then at worst you can make a random guess among them. This means that all you have to do is this:

$$ ACC_{lowerbound} = \frac{1}{e^{loss}} $$

So just exponentiate your loss and then divide one by it. Done.

# The bigger picture

So we now have three numbers to work with:

1. The accuracy as reported on our test set
2. The accuracy achieved by a baseline model
3. The estimate we have of how badly our model might plausibly perform in the wild derived above

Now it’s just a matter of judgement really. Given how well your model appears to perform, is the risk on the downside worth it?

Here's a scenario. You have a model with the following results:

1. Reported test set accuracy of 93% (implying 3% of upside on a baseline classifier)
2. A baseline accuracy of 90%
3. A lower bound estimate for accuracy of 75% (implying quite a lot of downside)

It looks like the model takes on quite a bit of risk for the upside it appears to be capturing, so you may think twice about putting this model into production. It’s not hard to think about another situation where the worst case accuracy is not far below a random baseline.

None of this is all that revolutionary. The aim is to think explicitly about how much trouble a model might cause in production. That's really the big deal here. Treating models like software means being clear-eyed about how they fail like software.

Finally, you can do this with other metrics aside from accuracy with some effort. Multi-class problems can also be addressed with a certain amount of jiggery pokery.

Hooray!


[^1]: Big caveat with this last one. If you're not respecting the word "simple", it probably shouldn't be a baseline. The idea is to work out how much better of you are compared to no model.
[^2]: You could use something else, though.
[^3]: Sure, it might not. 
[^4]: This is basically how adversarial attacks on ML models have become a thing. The more complicated models get, the more room there is for this. But this is an aside.
[^5]: Yup. Soundgarden jokes.
[^6]: https://en.wikipedia.org/wiki/Perplexity