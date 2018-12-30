---
layout: post
title: "Time series prediction with Recurrent Neural Networks"
comments: false
description: "post 11"
keywords: "time series, prediction, RNN, LSTM, GRU, recurrent, neural, networks, tensorflow, deeplearning"
---

![github_helper]({{site.url}}/material/2018/post_11/model_image.jpeg?raw=true){:height="350px"}

Hello Everyone!! In todays post I will be talking about a brief introduction on using **Recurrent Neural Networks(RNN)** for Time series prediction.  RNNs are a type of _Deep Learning_ models that are specifically well suited in handling temporal dependencies in data. For example, lets take the weather in a given day. If today is sunny, then there is some likelihood that tomorrow might be sunny too. Now obviously it might rain tomorrow, but the point is **what happens in the past, affects the future**. When we consider most phenomena in the natural world, we can see some temporal dependency in those datasets-like temperature, stock prices, signal strength variations or even video frames in a video segment. Knowing, that some processes is related across timesteps is not enough in most real world applications.

So the obvious next step is to predict what might happen based on some given historical data. And thats where _Machine Learning_ comes into the picture. You probably have heard of computers beating human champions in Chess and in other games like Go. **cont...**


##### So until next time,
##### Cheers!

**Prev: [Adding git support to Terminal]({{site.url}}/2018/git-support/)**
