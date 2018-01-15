---
layout: post
title: "Markov Chains 101"
comments: false
description: "post 8"
keywords: "Markov, Chains, pebble, game, chains, chain,introduction"
---

![markov-image](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2018/Post_8_MarkovCHains/first_image.jpeg){:height="300px"}

Hello Everyone!! in todays post I thought of writing an introduction for [Markov Chains](https://en.wikipedia.org/wiki/Markov_chain){:target="blank"}. Simply put, Markov chains are used to model systems that change randomly where a _current state_ is only dependent on the _previous state_.(_I'll explain what states are in a  minute_) In fact, its a pretty powerful technique used in fields ranging from **computer networks** to **statistical physics**. I'll explain the basics of Markov chains using a simple example called the _pebble game_ as illustrated above.

Now imagine we have a 3x3 grid just like the image above, with the **black dot** being a pebble. At each instance in time a person picks the pebble up and tries to throw to some other directly linked cell randomly.(Note that throwing the pebble to diagonal cells is not possible) The image below shows the three types of throws possible:

+ **`config (a) :`** The pebble is at the corner, So theres only two positions it can be thrown to.The pebble can't be thrown up or to the left.
+ **`config (b) :`** The pebble has three possible cells to be thrown to.The pebble can't be thrown to the left.
+ **`config (c) :`** The pebble can be thrown in all directions. 

![transitions](https://raw.githubusercontent.com/dherath/WebsiteMaterial/master/2018/Post_8_MarkovCHains/second_image.jpeg)

So the question is, _`lets say at each time step someone picks the pebble and throws to an adjacent cell and keeps on doing it. After 10,000 iterations of the process where would the pebble likely be? OR whats the probability of some cell having the pebble, provided this was done for a long time?`_ Now intuitively since there are 9 cells, and the person is going to keep on throwing the pebble in this space for a long time we can make a guess that the probability of finding this pebble in any cell is equally likely, i.e the probability will be $$ \frac{1}{9} $$. This is actually the correct result, but there might be problems so complex that getting these sort of insights might not be as intuitive, and that's where this technique truly shines. 

There are two main steps in defining Markovian models, the 1st is to **define the states** & the second is to **populate whats called a transition matrix**. Both of which I'll go through below.

### States

Before diving into the technique itself, there are some things called `states` that must be defined. 
> **States** refer to all the possible configurations of the system.

In our example, states refer to the cell position of the pebble at a given time instance. If you look at the figure again I've drawn an image with circles labeled **A-I**, these labels refer to the different cell  locations the pebble could be in. Furthermore, I've also drawn arrows, these arrows represent the possible transitions from one state(cell) to another. That image corresponds to all the possible things that could happen in this system of ours, and by definition nothing beyond those transitions should occur.

Lets take the initial state **A**, from this location if the pebble is to be thrown there are three possibilities,
1. A transition from A to B
2. A transition from A to D
3. No throw is possible up or to the left, therefore a transition from A to A

Similarly, the image represents all transitions in all states whom fall under the basic configurations explained in **(a), (b) & (c)**. Note that it's impossible to throw the pebble from A to E or from A to F, so there is no arrow corresponding to that.

> Figuring out the states of your problem is the hard part. Because there is not a set way in defining those, and it all comes down to how you see the problem. As you'll see in the section below what comes after that is way more simpler.

### The transition matrix

Now that we have our states defined, the second problem is the transitions.  It's all nice that our figure has arrows pointing to what might happen next. But _which of those possibilities actually happen?_ The thing to remember here is our entire system evolves randomly with time. Any of the state transitions could  happen at some instance. Therefore **the transitions aren't deterministic rather they are probabilistic**. Meaning there is a probability value associated with each transition from one state to another.

Ok, now how do we get those probabilities. First of all since the throws are done randomly and independently of each other. **config (c)** shows the best possible case where a pebble could be thrown in all four directions. Since any of these transitions is equally likely $$ P_{}






##### So until next time,
##### Cheers!

**Prev: [Proving correctness of Algorithms](http://dinalherath.com/2017/Proving-Correctness-of-Algorithms/)** 
