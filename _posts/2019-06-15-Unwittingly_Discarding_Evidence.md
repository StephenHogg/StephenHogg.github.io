---
layout: post
title: "How to gather a bunch of evidence and then ignore it"
---

Oh my god this happens all the time I swear. If you're working in machine learning then it is unavoidable that you work in the presence of uncertainty. This isn't such a bad thing, but how we think as humans sometimes works against us when dealing with uncertainty. This post will look something that commonly goes wrong and more importantly, how to spot it so you can do something about it.

Everyone's different[^1], so maybe this advice won't work for everyone. But that's fine.

# What's the story?[^2]

When building a model it's easy to get caught in a narrative fallacy. This was described in _The Black Swan_ by N. N. Taleb as follows:

> "The narrative fallacy addresses our limited ability to look at sequences of facts without weaving an explanation into them, or, equivalently, forcing a logical link, an arrow of relationship upon them. Explanations bind facts together. They make them all the more easily remembered; they help them make more sense. Where this propensity can go wrong is when it increases our impression of understanding."

The problem is, this is really pervasive. And like any kind of absolutely normal background noise, it can sometimes to be hard to spot and focus on.

# Thinking is hard :(

Fair enough. Machine learning models can be big complicated things, so knowing what's going on in them is an active field of research in its own right, not just an onerous task for the practitioner. An easy way to catch yourself succumbing to a narrative fallacy is to look for yourself saying _"I know what's going on here"_, or words to that effect.[^6] This is because if you're saying that you're potentially focussing on the rare delight of being right, as opposed to sticking to the task of working out what you still don't know. Try getting into the habit of talking about the state of your knowledge without referring to yourself and see how it changes your view.[^3]

I don't think any less of anyone for thinking like this to be honest, large parts of an ML person's job consist of being wrong. Wanting a win every now and then is only human. Problem is, a lot of the time when you think you've got it all sorted out, you're actually shooting yourself in the foot at that very moment. It can really be a dirty, difficult job. So keep an eye on yourself if you find yourself desperate for a breakthrough, you might inadvertently join the dots in a way that allows you to hallucinate one. 

# Performance statistic hell

Turn it up to 11 if you find yourself deliberately glossing over any piece of evidence at your disposal because it conflicts with your understanding of your progress.[^4] As a rule, I generally tend to track a number of different metrics when training a model and look for situations where their results conflict. Log loss going down but F1 going down with it? This incongruity is the sort of thing you want to know about, rather than disregarding one of these numbers because it doesn't fit a proposed explanation about the functioning of your model. Go hunting for a mess in your performance statistics, just don't over-interpret the evidence you have. 

A handy way to do that is to not let yourself get away from the definitions of the metrics you're working with. Let's work through the above example. In a classification setting, log loss is calculated as the logged distance between the prediction and label. So if that on average decreases, fine, predictions are closer to the actual labels _on average_. The words "on average" are important because they ignore what your labels are - so shifts in log loss can be explained by an overall shift in the distribution of predictions created by your model. F1 gives you a blended measure of your model's precision and recall. If F1 goes down, at least one of precision and recall went down. So you should inspect the confusion matrix to see what has changed. If it turns out that your predictions have become biased, it will appear here. If that's not the case, then you can attach a lower probability to biased predictions being the cause of your results and instead look for outliers skewing your average loss result. This is a very different thought process to picking parts of the model and hypothesising about how they may have influenced your performance statistics.

[AutoML seems like a good way around all of this, but in my opinion it's an iron law that in any situation a sufficiently innovative and eager person can always find a way to shoot themselves in the foot. You still need to be clear about what you're up to.](https://breakitdownto.earth/2019/06/12/Automated_Mistakes_with_AutoML.html)

# Don't believe the hype[^8]

A textbook-definition narrative fallacy I see _everywhere_ consists of pretending your neural network functions the same way as a human brain and consequently believing that if you replicate your own decision-making process in constructing the network then all will be well. When it inevitably blows up temporarily or gives weird results - because it is in fact not a human brain - all of a sudden it's very difficult to know what to do because that whole frame of reference constrains thinking. Stop doing this![^5] Of course there are plenty of very, very smart people who use the human brain analogy to educate others about how neural nets work, but that doesn't mean you should consider it any kind of literal truth when building one yourself. Remember, that analogy is a simplification used for the purposes of education. No-one has an LSTM unit in their head.[^7]

# Baby steps

One simple thing you can do to avoid falling for narrative fallacies is to slow down the process. I get it, your boss is an arsehole and you have to keep it moving. What I'm saying is that if you're caught in a narrative fallacy, there can often be a strong urge to make multiple changes to your model at the same time, interpret whatever evidence you get as confirmation of the working hypothesis you had and then repeat this process. Again, this can be made worse by the rancid breath of your boss on your neck.

Even worse, the real danger is that you wind up going around and around in circles without realising it due to a lack of clarity about the reasons for the effectiveness or otherwise of the changes you make, or in the worst case a lack of clarity about what you've even tried. Or you can wind up going round and round in circles, only to find a way out of it by means of another fallacious narrative that conveniently explains everything (but isn't actually right). Occam's Razor is pretty clear that sometimes the simple explanation can be the wrong one.

Instead, force yourself to make only one change at a time. This does two things for you:

1) It makes whether or not your change is a good one much clearer, and
2) It allows you to work out what to do next, because you now know precisely what to ascribe success or failure to.

If you make three changes to a model, train it, then find the results are better - what was responsible? Like as not there's nothing that really tells you, so the blanks get filled in subconsciously instead. Look at the functioning of your model at a lower level where possible and leave overarching narratives to themselves. Don't leave room for the imagination by not trying to keep too much in your head at once and let it be an alarm bell if you find yourself really hankering to make a few changes at the same time. It can definitely feel like you're moving a lot slower, but that's because there's a false economy in the alternative. Trying a scatter gun approach with a bunch of changes might feel like a quicker path to a result but not if you stop and consider all the time spent in that approach not being clear about what's going on.

This shouldn't be news to anyone from a scientific background. But we aren't all, are we? And even if you are, it's important to make sure that these habits of mind are explicit, not tacit. It's the unspoken parts of the train of thought that are at issue here.






[^1]: of course
[^2]: ...[morning glory](https://www.youtube.com/watch?v=Wm54XyLwBAk)
[^3]: The reason for doing this is that _you are not your code_. Keeping some mental distance from your code and models can help you think more freely about them.
[^4]: Being able to spot yourself doing this and act is the hard part. In all seriousness, have a look at some cognitive behavioural therapy material. It's not just for depressed people, it can help you work more effectively with your internal monologue and state of mind and not let this sort of thing slide through.
[^5]: If you've succeeded in building a model like this, well done. But are you sure you succeeded because you had the right approach? There might be cases where you explicitly do want to build a model to replicate some easily-understood process or object - was that so in your case, or is it the case that thinking that having an overarching narrative was the key to success is actually a narrative fallacy in its own right? That's how pervasive this sort of thing can be. 
[^6]: This isn't meant to be snark.
[^7]: Maybe Schmidhuber does.
[^8]: Yup. Public Enemy jokes.
