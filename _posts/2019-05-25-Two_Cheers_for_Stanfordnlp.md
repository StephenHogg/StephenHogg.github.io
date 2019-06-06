---
layout: post
title: "Two Cheers for StanfordNLP!"
---

As you may or may not know, the [Universal Dependencies Github repo] is an absolutely wonderful source of tagged NLP data that can be used for a wide variety problems. It's worth reinforcing, it's a great resource and an example to us all about where academic collaboration can lead.

So it's nice to see people doing stuff with it. In particular, this means the latest work done in PyTorch by the [Stanford NLP group]. Have a look around and you'll see a very large range of pretrained models put together to solve quite a few different tasks. Look at the system performance page and you'll see that they all work pretty well, too.

What's the drawback, then?

## What if we tried something simpler?

One reasonable thing you might ask yourself is - how much better do these models perform than a much simpler version that accomplishes the same task? It's actually pretty easy to get an answer to this, it turns out.

One of the prior works of the Stanford guys was [CoreNLP], which was originally written in Java and didn't use any kind of neural network at all. Instead, it used [Conditional Random Fields], which are a kind of probabilistic graph. Leaving almost all of the differences between a CRF and the LSTM-based neural network approach aside, take it as read that the models you can use in CoreNLP are a lot, lot simpler.

All we really need to do is get the underlying data that was used to generate the PyTorch models and chuck it into CoreNLP and see what the results tell us.

## Results!

For the purposes of this discussion, let's focus on POS (part of speech) tagging. There are two reasons for this:
1) That's why I was doing this in the first place, and
2) It's a pretty common problem

Here's a small table with accuracy stats for a few corpora from the Universal Dependencies repo.

| Corpus        | Pytorch           | CoreNLP  |
| ------------- |:-------------:| -----:|
| UD_Vietnamese-VTB    | 79.5 | **87.7** |
| UD_Indonesian-GSD     | 93.7     |  **96.6**  |

For the record, the architecture options used for the CoreNLP models were:

GET ARCH AND INSERT HERE

The more interesting thing than the details of these particular models is that they are outperforming the LSTM-based approach. That is, they're both (heaps) faster and more accurate for this task using this dataset. Yes, this approach doesn't consider every possible language, but hopefully with a few languages the point is already coming across.

So now what?

## Two cheers

This post isn't meant as an attempt at knocking StanfordNLP or anyone associated. Very far from it. The Stanford NLP group did us all a favour by putting these models together, not just because it gives you something to work with but also because in order to make progress in this field we actually have to try stuff out at some stage. Leading by doing and actually putting together a bunch of models on the back of UD data is a great way to encourage the usage of that dataset. They're also owed a debt of gratitude for having done CoreNLP before that, which I personally use and find extremely handy. 

Instead, the point of this exercise was to suggest that some of the problems we face in the field of machine learning aren't going away. Bigger isn't necessarily better when it comes to model complexity and any result needs to be viewed in context of a reasonable baseline. A lot of machine learning is a long, slow plod that you kind of just have to go through. But that doesn't necessarily mean any part of it isn't worth it. 



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [Universal Dependencies Github repo]: <https://github.com/UniversalDependencies>
   [Stanford NLP group]: <https://stanfordnlp.github.io/stanfordnlp/>
   [CoreNLP]: <https://stanfordnlp.github.io/CoreNLP>
   
