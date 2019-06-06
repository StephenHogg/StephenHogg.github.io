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

Lol
