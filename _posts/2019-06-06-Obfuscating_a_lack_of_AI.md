---
layout: post
title: "How to obfuscate the fact that you're not really doing AI"
---

Oh my god this happens all the time I swear. What I'm talking about here is the thing where you build a model and think it works, but if you look closer it's actually doing almost nothing. This post looks at a few dead giveaways and traps you (or better yet, someone else), can fall into.

## Even simple models can stuff up

Once upon a time I saw a logit model that was built to predict customer churn. The relevant group in charge of it had performance stats to back up their assertion that it worked well. But a quick glance suggested all was not as it seemed.

What gave this away? It's pretty simple, in fact. The variables of the model were all pretty straightforward - indicators for variables, some customer history variables and some other stuff to handle the frequency of their interactions with the company. So far so good. The problem with all this becomes apparent when you look at the coefficients of the model. Almost all of them were near zero, except for the dummy variable for one product which was massive.

In other words, the model was just one giant `if` statement. If you had this product, you would churn, otherwise you wouldn't. The reason this model seemed like it was ok was because customers with that particular product were indeed churning _en masse_, such that it masked performance flaws elsewhere in the sample space.

In the course of a few months' worth of trying to alert people to this, I realised that to accomplish that aim you need a good explanation for how that could have happened in the first place. This brings us to the villain of this particular story, a thing called _quasi-separation_.

### Separation anxiety

[This page](https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faqwhat-is-complete-or-quasi-complete-separation-in-logisticprobit-regression-and-how-do-we-deal-with-them/) gives as good an explanation as any I've seen as to what's going on here. Long story short, the dataset used to build the model has a severe bias in it, such that it's possible to make predictions about the label with 100% confidence in some circumstances. 

In the case I described above, what had happened was that the model was trained on a dataset that _contained no examples of a customer not churning and also not having that one product_. So maximum likelihood estimation takes that and runs with it and you wind up with a model that's ridiculously oversensitive to this one variable. The confusion matrix shows this more clearly:

| churn | no churn |
Has product | 125 | 0 |
Doesn't have product | 20 | 50 |
