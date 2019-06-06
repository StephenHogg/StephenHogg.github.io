# Transformers: more than meets the eye? (Part 1: The Past)
There's quite a lot of talk about how wonderful Transformers are and how they solve a lot of problems. Fair enough, they are pretty good. That said, all the explanations I've seen so far include math and neural network diagrams (nothing wrong with that!). What I'm going to attempt to do is talk about how they work in a more conceptual way, because it's much easier to understand the math and diagrams if you have some idea of why those equations even exist.

In this post I'll attempt to walk through the history that got us to the point where Transformers (the neural network technique, for clarity), seemed like a good idea. There are a couple of things we'll need to think about:

* The situation we use a Transformer in - and why
* How have we evolved in thinking about how to deal with natural language?
* Why wasn't any of the stuff we thought of in the past good enough? Why did we have to keep going and invent transformers?
* How do transformers work?

We'll look at the first two points in this post and the second two in the next post. I'll be assuming you know what you're doing with neural networks, to at least some extent.

Hopefully what you'll see at the end of all of this is that Transformers contain echoes of all the things that came before and that in conceptual terms they're actually quite simple. Finally, I'm going to talk about this through the lens of Natural Language Processing (NLP), because that's what these things get used for. If you're interested in this with respect to financial time series stuff or otherwise, just squint really hard and imagine some of the words are replaced with whatever the appropriate domain-specific replacement is.

## What problem is a transformer meant to solve?

This is actually the simple bit of these posts, if anything is. It's what is known as  a _sequence to sequence_ problem. Also known as a _seq2seq_ problem if you're one of the people who works on this sort of thing.

Now, what the heck is that?

Basically, it's the sort of thing you see over and over in NLP. Translation is a perfect example. Take for instance the following input and output pair:

>Input : I do want to eat vegetables
>Output: 我想吃蔬菜

The goal of this task is to turn the input (English), into the output (Mandarin). Clearly, the input is just a bunch of words and so is the output. BUT! The order in which they appear matters. To see this in action, the input "do I want to eat vegetables" clearly has a different meaning. Some languages might have less of a problem with this than others, but in any event it's a real source of information that we want to incorporate when we're working on this problem. So the challenge is, how to predict a sequence of values - not necessarily words, it could be a financial time series problem you're working on - using not just the knowledge of the input values but their structure (i.e. order), as well.

Just to briefly emphasise, this general type of problem has existed forever. People creating neural networks didn't invent this type of problem, only new ways of solving it.[^2]

### Important digression!
Looking at the above example and a great deal of explanatory material on the topic of _seq2seq_ problems, there's a common problem you can encounter. It's this: the problem looks like the input and output are concurrent, but they actually aren't.

The way the problem works is, you feed in an input sequence and then want your model to complete the sequence. So really, the input and output pair above should be presented more like this:
> I do want to eat vegetables __BREAK__ 我想吃蔬菜

The reason for the __BREAK__ there is that you need something to tell your model to stop reading input and start generating output.

This will become very important as time goes on in this discussion.

## Baby steps
Ok so first let's step back in time.[^1] In the beginning (and I mean _actually_ a long time ago, like 40 years or more), we didn't have any of the gleaming mathematical machinery we now do for working on language problems. So where to start?

### N-grams 
This was the first, and simplest go at trying to figure out the _what comes next?_ problem beyond just feeding in your input and hoping for the best. The idea here is that you can actually do a better job of predicting the next word if you use not only the current one, but the one before it. All the "N" in "N-grams" tells you is that you might use more or less context as opposed to specifically one or two words of history. The following examples might make things clearer.

Guess the next word given the input:
> is

This is basically impossible, right? There's some stuff that might not be that likely to come next, but by and large we can't really narrow it down. 

What about this input:
> weather is

This is a bit more workable. We could probably make a few guesses about what goes next, but it's definitely a narrower scope of possibilities than last time.

Now what about this:
> The weather is

At this point I'm fairly sure something like _hot_ or _cold_ comes next. 

So far so good, but what's the cost? It's pretty simple, in fact. Firstly, the reason we know one of those words comes next is because we've all watched too much news on the TV so far in this life. That's well and good for a human, but sometimes you don't have enough data for that to work for a machine. 

Another problem arises if you're trying to predict more than just the next word. If you're trying to predict a whole sentence, you're in a lot of trouble. Maybe you can get the first word of your output correct, but after that you're at the mercy of whatever you predicted as your first word. If that's wrong, everything else becomes even wronger. We've only really started solving this problem comparatively recently.

Even worse, the longer your input sequence the rarer it is! In the case of "The weather is", you might be able to see it a few times in a dataset if you're lucky. But not as many times as you see "weather is", perhaps. So we're stuck in a classic problem where we can get a few edge cases right all of the time, or have hopefully better than random performance over a much broader set of cases, assuming your input doesn't fundamentally change as time goes on. That's probably not good enough. So people kept researching stuff.

### Time becomes a loop[^3]
Another thing that people discovered when talking about _seq2seq_ problems is that sometimes stuff a long time ago in your input sequence actually matters in terms of the prediction you make at the end of it. Doing stuff with N-grams won't work here because for example a 128-gram is basically unique. You'll only every see that sequence of tokens the once, if at all, so it's no use for prediction. So what can you do about this?

This is where things start getting complicated, unfortunately. That is to say, as soon as you try and do anything beyond the most basic stuff with a _seq2seq_ problem, it gets complicated.

Intuitively, what we want is something that can remember the earlier parts of a sequence like this:[^4]
>I was born in a water moon. Some people, especially its inhabitants, called it a planet, but as it was only a little over two hundred kilometres in diameter, 'moon' seems the more accurate term. The moon was made entirely of water, by which I mean it was a globe that not only had no land, but no rock either, a sphere with no solid core at all, just liquid water, all the way down to the very centre of the globe.
>
>If it had been much bigger the moon would have had a core of ice, for water, though supposedly incompressible, is not entirely so, and will change under extremes of pressure to become ice. (If you are used to living on a planet where ice floats on the surface of water, this seems odd and even wrong, but nevertheless it is the case.) The moon was not quite of a size for an ice core to form, and therefore one could, if one was sufficiently hardy, and adequately proof against the water pressure, make one's way down, through the increasing weight of water above, to the very centre of the moon.
>
>Where a strange thing happened.
>
>For here, at the very centre of this watery globe, there seemed to be no gravity. There was colossal pressure, certainly, pressing in from every side, but one was in effect weightless (on the outside of a planet, moon or other body, watery or not, one is always being pulled towards its centre; once at its centre one is being pulled equally in all directions), and indeed the pressure around one was, for the same reason, not quite as great as one might have expected it to be, given the mass of water that the moon was made up from.
>
>This was, of course,

Imagine you're trying to guess what comes next after "This was, of course,". Do you think it's something about the physics stuff towards the end of the passage, or about the perspective of people who live on planets where ice floats on the surface referred to much earlier in the text? It could be either, but if your model isn't capable of having some way of hanging onto relevant info from much earlier in your input sequence, you have no choice. You can only really consider the physics option.

So we needed some way of hanging onto not everything but at least some important info from the earlier parts of a potentially long sequence. This is where neural networks start to play a role.

The original go at this involved trying to get a neural network to have a memory of its own, after a fashion.[^5] I don't want to go on forever about this because it turns into talking about math, but the long and the short of it was that you wanted a bit of your network to loop around on itself in a way that made some of the information coming in from a given sequence element take a while to get back out again. 

It's a bit like Gumbo. [^6] This is a slightly weird analogy, but stick with me. Gumbo is this dish you get in the southern parts of the U.S. that takes _forever_ to cook. But the trick is to make it so that the flavour of the ingredients you put in early on is still retained some hours later in the pot when you finally finish cooking, even if you've taken that ingredient back out.

In our case, we want to put words in and move on to subsequent parts of the sequence without necessarily losing all of the earlier flavour. By the time we get to the end of that passage I put in above, we still want to be able to have some hint of the earlier part where the speaker says his planet was a moon.

In practical terms, what you do is make information take a really long path to get out of your network. Problem is, this isn't perfect either. For a really long sequence, you can wind up with a gigantic number of parameters in your network. You also don't really know what to hang on to, so by creating a recurrent neural network all you're really doing is trying to hang on to as much of your input information as possible for as long as possible. This is on top of the other problem where introducing recurrence makes it slower to process an input sequence because now you have a dependency problem: you can only process some of your input after you've processed the bits that came before.

That said, it's still a big big step forward.

### My model accurately predicts everything!
The next step forward after recurrence seemed at first like it solved everything. We'll see that wasn't the case though. 

It turns out two of the problems with the basic approach to recurrence can be solved in the same way. The non-selectiveness of memory storage in a basic recurrent net and the escalating number of parameters needed were both addressed by the Long Short-Term Memory cell. 

What this thing did differently was conceptually simple enough. Rather than just adding links between cells in a neural network so that it took a while for information to find the exit, each cell now got its own memory storage. 

As always, so far so good. With this particular invention, you could get to the end of a passage like the one in the previous section and have some sort of useful numerical information from earlier on predict what comes next.

Going back to the first example I gave:
> I do want to eat vegetables __BREAK__ 我想吃蔬菜

Now that we have an LSTM to work with, the input sequence can comfortably be quite large and we'll still have all of it to work with when we start predicting an output sequence. 

That's another big step forward, but there's still a problem here. Now, although we have a lot of information to work with when we start predicting an output sequence, we still have the problem that the sequence is only as good as the first prediction. 

That is to say, we need the entire sequence to be meaningfully encoded in whatever you have after you've looked at the last item in your input. It also has to be able to let you spell out the entire output sequence. And when you do, you're still stuck with the problem that your second prediction depends on your first one and your third prediction depends on your second one. 

Also this LSTM stuff is relatively slow because you have to process one element of your sequence at a time and there's no real way around that in the framework. That said, as always, it was a big leap forwards and started to show some serious potential for dealing with _seq2seq_ problems.

Wouldn't it make more sense and potentially be faster if we could use all of the bits of the input sequence independently in determining an output, instead of pancaking the information you have up against an invisible wall separating your input sequence and whatever comes next? This question is more or less what the Attention method and Transformers grow out of. I'll talk about why next time.


[^1]: This is secretly a joke. If you work out what I'm referring to, I'm not sorry.
[^2]: Just in case anyone was wondering.
[^3]: [https://www.youtube.com/watch?v=DNb4VKln1uw](https://www.youtube.com/watch?v=DNb4VKln1uw)
[^4]: From _The Algebraist_ by Iain M. Banks. R.I.P.
[^5]: Not as cool as anything invented by Miles Bennett Dyson, but still.
[^6]: [https://en.wikipedia.org/wiki/Gumbo#Preparation_and_serving](https://en.wikipedia.org/wiki/Gumbo#Preparation_and_serving)
