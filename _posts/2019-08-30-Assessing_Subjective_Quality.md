---
layout: post
title: "Qualitative Assessment is a Nightmare"
---

Last week I had an idea about maybe using FaceNet or some other Siamese network to create word embeddings. Turns out [plenty of people](https://www.researchgate.net/publication/321302050_Beyond_Word2Vec_Embedding_Words_and_Phrases_in_Same_Vector_Space) [have had](https://chauff.github.io/dir2016/accepted-submissions/kenter.pdf) [that idea](https://github.com/dhwajraj/deep-siamese-text-similarity), or some variant thereof. So doing it myself looks a bit silly.

There's still something to think about here: how does one decide whether word vectors are good or not? The obvious way to look at this is to ask yourself whether they let you do the task you need them for. For someone wanting to make a library of pre-trained vectors available (such as those of [fastText](https://fasttext.cc/docs/en/crawl-vectors.html), for example), it isn't as simple. You might try comparing two libraries of word vectors across a number of tasks, or maybe even doing the old [word analogy trick](https://kawine.github.io/blog/nlp/2019/06/21/word-analogies.html).

More broadly, how do you do something about assessing the _quality_ of a machine learning solution when reasonable people can differ on the answer?

# Sometimes it's easiest to bury your head in the sand

We know how to measure model performance in objective terms, but if you're interested in something subjective it's easy to waste your time learning nothing. The problem with subjectively assessing the output of a machine learning model is precisely that.

The bog standard thing people do in this situation (in my experience), is decide to look at a sample of data manually and get a human to make a definitive judgement about whether the model performed well or not. I prefer to think of this as "pretending there isn't a problem". By getting a human to make a definitive judgement, you're implicitly saying that the person involved is always right and discounting the possibility of other viewpoints. The common (in my experience) answer to this problem is also naïve. Getting a few humans to check and agree on how they will assess things doesn't solve anything. When people inevitably disagree, who is right?

The even bigger problem here is that inevitably, when you're verifying things manually it's hard to check more than a little data. This is _definitionally_ the most labourious approach for verifying the performance of a model!

# Well that didn't work

At this stage, it's natural to start looking for alternatives. Rather than looking for definitive proof that a model works (or doesn't), instead it's better to just look for _evidence_. This is where the word analogy thing comes in again. It's a perfect example of what to do, in fact. Start with an initial idea of something that should be desirable in the outputs you have and then check whether that's the case. Then come up with something else that intuition suggests should emerge from the results you have generated. Test it and move on. Then it's just a matter of keeping going until you've got enough bits of evidence to feel like they add up to something.

One of the reasons the word analogy trick is such a great example is that [sometimes it shows you bad results](https://books.google.com.au/books?id=_LBmDwAAQBAJ&pg=PA40&lpg=PA40&dq=fasttext+king+queen&source=bl&ots=nl1uX3NRpR&sig=ACfU3U32Y2i_j5fyoFDnKtwPt13r1271UQ&hl=en&sa=X&ved=2ahUKEwiUoIC5rafkAhXp7HMBHSzRCtUQ6AEwGXoECAkQAQ#v=onepage&q=fasttext%20king%20queen&f=false). If that happens, it's a simple matter to decide a) whether that matters to you or not and b) how it colours your view of whether this model works or not.

I find this approach works better for a few reason. The first is that you wind up assessing a lot more data, because it's a much less labourious approach. That in turn should reduce the scope for nasty surprises down the track. The second is that this explicitly accepts the subjective nature of the problem. By not looking for binary, definitive proof and instead just amassing indications, the fact that different people can have different views isn't necessarily as big of a deal.

I'll be gone for the next little bit but should be back at the end of September!