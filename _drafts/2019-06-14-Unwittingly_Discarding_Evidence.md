---
layout: post
title: "How to gather a bunch of evidence and then completely ignore it"
---

Oh my god this happens all the time I swear. If you're working in machine learning then it is unavoidable that you work in the presence of uncertainty. This isn't such a bad thing, but how we think as humans sometimes works against us when dealing with uncertainty. This post will look something that commonly goes wrong and more importantly, how to spot it so you can do something about it.

Everyone's different[^1], so maybe this advice won't work for everyone. But that's fine.

# What's the story?[^2]

When building a model it's easy to get caught in a narrative fallacy. This was described in _The Black Swan_ by N. N. Taleb as follows:

> "The narrative fallacy addresses our limited ability to look at sequences of facts without weaving an explanation into them, or, equivalently, forcing a logical link, an arrow of relationship upon them. Explanations bind facts together. They make them all the more easily remembered; they help them make more sense. Where this propensity can go wrong is when it increases our impression of understanding."

The problem is, this is really pervasive. And like any kind of absolutely normal background noise, it can sometimes to be hard to spot and focus on.

# asdfafd

Fair enough. Machine learning models can be big complicated things, so knowing what's going on in them is an active field of research in its own right, not just an onerous task for the practitioner. The easiest way to catch yourself succumbing to a narrative fallacy is if you ever say _"I know what's going on here"_, or words to that effect to yourself. This is because if you're saying that you're potentially focussing on the rare delight of being right, as opposed to sticking to the task of working out what you still don't know. Try getting into the habit of saying that without referring to yourself and see how it changes your view.[^3]

I don't think any less of anyone for thinking like this to be honest, large parts of an ML person's job is being wrong. Wanting a win every now and then is only human. Problem is, a lot of the time when you think you've got it all sorted out, you're actually shooting yourself in the foot at that very moment. It can really be a dirty, difficult job. So keep an eye on yourself if you find yourself desperate for a breakthrough, you might inadvertently join the dots in a way that allows you to hallucinate one. Turn it up to 11 if you find yourself deliberately glossing over any piece of evidence at your disposal because it conflicts with your understanding of your progress.[^4] 

[AutoML seems like a good way around this problem, but in my opinion it's an iron law that in any situation a sufficiently innovative and eager person can always find a way to shoot themselves in the foot. So it isn't a way around these pitfalls, in my view.]()

The other textbook-definition narrative fallacy I see _absolutely everywhere_ consists of pretending your neural network functions the same way as a human brain does. When it inevitably doesn't - because it is in fact not a human brain - all of a sudden the practitioner immediately don't know what to do because their whole frame of reference just became invalid. Stop doing this! Of course there are plenty of very, very smart people who use the human brain analogy to educate others about how neural nets work, but that doesn't mean you should think about it that way when building one yourself. Remember, it's an oversimplification used for the purposes of education.

# Baby steps

One simple thing you can do to help stop this is to slow down the process. I get it, your boss is an arsehole and you have to keep it moving. What I'm saying is that if you're caught in a narrative fallacy, there can be a strong urge to make multiple changes to your model at the same time, interpret whatever evidence you get as confirmation of the working hypothesis you had and then repeat this process. Again, this can be made worse by the rancid breath of your boss on your neck.

Even worse, the real danger is that you wind up going around and around in circles without realising it if you aren't clear about the reasons for the effectiveness or otherwise of the changes you make building a model. Or you can wind up going round and round in circles, only to find a way out of it by means of another fallacious narrative that conveniently explains everything.

Instead, force yourself to make only one change at a time. This does two things for you:

1) It makes whether or not your change is a good one much clearer, and
2) It allows you to work out what to do next, because you now know precisely what to ascribe success or failure to.

If you make three changes to a model, train it, then find the results are better - what was responsible? Like as not there's nothing that really tells you, so the blanks get filled in subconsciously instead. Don't leave room for the imagination and let it be an alarm bell of a potential narrative fallacy if you find yourself really hankering to make a few changes at the same time.

This shouldn't be news to anyone from a scientific background. But we aren't all, are we?

# One more thing





[^1]: of course
[^2]: ...[morning glory](https://www.youtube.com/watch?v=Wm54XyLwBAk)
[^3]: The reason for doing this is that _you are not your code_. Try to keep some mental distance from your code and models, it will help you think more freely about them.
[^4]: Being able to spot yourself doing this and act is the hard part. In all seriousness, have a look at some cognitive behavioural therapy material. It's not just for depressed people, it can help you work more effectively with your internal monologue and state of mind and not let this sort of thing slide through.
