---
layout: post
title: "A random thought about FaceNet"
---

The problem of facial recognition is now pretty much solved thanks to [FaceNet](https://arxiv.org/abs/1503.03832).[^1] The underpinning insight that makes it all
come together is analogous to the way an SVM works. But have we done all we can with this rather novel form of network?

Rather than feeding in one example at a time with a corresponding label, in the FaceNet architecture three examples are presented with the intention that
[one of these things is not like the others](https://www.youtube.com/watch?v=rsRjQDrDnY8). The loss function just tries to make sure that the ensuing model respects that fact for a 
given triplet of examples, similar to how an SVM just tries to maximise the margin between classes rather than accurately predict the value for every single observation.

As someone working in NLP, I immediately wondered about the possibility of using this technique to encode word vectors. Not only that, but whether they would be worthwhile or not.
A little searching on the internet makes it appear to me that this hasn't been done, so over the next week or so I will attempt it. Prior to setting out, 
here are a few thoughts:

- Where the hell do I even get a dataset from?
- Are we recording enough information about the relationship?
- Is a max-margin approach really going to give us the fine-grained control we want?
- How do I tell if this was a waste of time?

As usual, I predict the first of these things will take the most of my concentration. That's just how this machine learning caper works.
More on this next time. 

The second thing makes me wonder a bit. Normally when building word vectors, you work with co-occurrence of terms rather than explicitly with synonym relationships as implied by how FaceNet works.
I wonder if this is really sensible, as it may constrain the types of information that can be encoded in a vector. That said, would this prove more useful for classification tasks?
That seems to be one of the primary uses for FaceNet embeddings and they're very, very handy in that setting.

Thirdly, the max-margin thing. The classic way of explaining why word vectors are worth the bother involves adding and subtracting them to then [pretend they give you a reasonably intuitive answer](https://twitter.com/goodfellow_ian/status/1133528189651677184?lang=en).
This property could potentially be disturbed by max-margin learning, because within a given set of synonyms the learning process wouldn't necessarily make any attempt
at organising the individual elements. On the other hand, a thesaurus can be regarded as a really massive pile of partially-overlapping sets, so this may not actually be a problem after all.

The last problem is the most annoying, because this boils down to qualitative analysis. I've got another whole blog post in mind about why qualitative analysis is a minefield and what can be done about it,
but for now let's just say that the problem here is that we can't necessarily say definitively whether one set of embeddings is better than another.

Anyway, that's what I'm going to try - very curious to see how it turns out!

[^1]: If you want a simpler explanation of how FaceNet works, [check this out](https://omoindrot.github.io/triplet-loss).
