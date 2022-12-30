---
layout: post
title: "Explaining Graph Neural Network (GNN) based Malware Classification"
comments: false
description: "post 16"
keywords: "gnn, graph, neural, network, classification, malware, control flow graph, cfg, deep learning, explainable AI, AI, machine learning"
---

Hi All!! today I will be writing about another piece of research I completed as part of my PhD. The entire premise of this work revolves around [explainable-AI](https://en.wikipedia.org/wiki/Explainable_artificial_intelligence), specifically in the domain of cybersecurity. In recent years there has been an increasing effort of utilizing Machine Learning and Deep Learning models for cybersecurity applications, ranging from intrusion detection to malware classification.

![graph-explanations]({{site.baseurl}}/material/2022/post_16/expl.jpeg?raw=true){:width="800px"}

However, most of these state-of-the-art deep learning models are treated as black-boxes, meaning that we aren't able to explain why a given model predicts some malicious activity, which makes it hard for an analyst or threat hunter to identify if an alert is truly malicious. To circumvent this issue there has been a growing interest in explaining deep learning models used for cybersecurity tasks. In my PhD work we pushed the boundary in explaining deep-learning based malware classification by introducing an explainer named `CFGExplainer` ([paper](https://www.dinalherath.com/papers/2022dsn.pdf), [code](https://github.com/dherath/CFGExplainer)). 

[Graph Neural Networks](https://blogs.nvidia.com/blog/2022/10/24/what-are-graph-neural-networks/) have shown great promise in malware classification tasks, where the malware source code is processed and presented in a graph format called a `Attributed Control Flow Graph (ACFG)`. However explaining how these detections work is hard, mainly because a given malware graph can have over thousands of nodes and edges. Identifying which exact portion of the graph (i.e., subgraph) represents malicious code while pruning out the less important bits is the main challenge addressed in this work.

### Malware classification with GNNs

![acfg]({{site.baseurl}}/material/2022/post_16/acfg.jpeg?raw=true){:width="640px"}

In this first section, I will go through a brief overview of how source code is converted to a graph format for our detection task. Typically, in a `Attributed Control Flow Graph` nodes represent basic blocks of code that have atomic executions as shown in the image above. The edges between these basic blocks are the connectivity through `call`, `jump` instructions or of how the code flows through from one block to another. For each node, we define node features based on the type of instructions present within the code block.

![acfg]({{site.baseurl}}/material/2022/post_16/gnn.jpeg?raw=true){:width="600px"}

After this step, the graphs are processed by the Graph Neural Network model. A GNN model usually operates in two stages. First it processes the node/edge features and the spatial connectivity in the graph to produce `node embeddings`. These node embeddings are latent representations of nodes that capture information useful for some subsequent task, in our case the node embeddings contain important information with respect to malware classification. Then in the next stage the node embeddings are processed by a feed forwarding neural network that produces classification probabilities based on the malware types.

### CFGExplainer

![cfgexplainer]({{site.baseurl}}/material/2022/post_16/cfgexpl.jpeg?raw=true){:width="780px"}

The figure above shows the architecture of our solution. In our work, we assume that there exists some GNN model that is capable of classifying control flow graphs into their respective malware types. Initially the graph sample to be explained is processed by the GNN classifier, which produces both the node embeddings and the malware class label. Then these embeddings, label and the original graph is provided to CFGExplainer. 

CFGExplainer operates in two stages. First in an **initial learning stage**, the explainer learns to score nodes with respect to their contribution towards malware classification. Then in the second stage the explainer prunes out nodes that have the least importance. This pruned subgraph is provided as an explanation to the analyst along with an ordering of nodes based on importance to classification.

The learning stage is carried out through two interconnected neural network components (a node scoring module and a surrogate classifier) that are jointly trained to identify important nodes. In the forward pass in this algorithm,

![forward-pass]({{site.baseurl}}/material/2022/post_16/learning.jpeg?raw=true){:width="620px"}

1. First the node embeddings are processed and a score is produced for each embedding. Here a larger score correspond to the node being viewed as more important.
2. Then the scores are multiplied against the original node embeddings to produce a weighted node embedding per node.
3. Finally, these weighted node embeddings are fed through a second neural network module (i.e., a surrogate classifier) that produces classification probabilities for the malware families.

After producing the classification probabilities, the backward pass is carried out as a back-propagation step where the objective is to mimic the malware detection capability of the original GNN model through this surrogate classifier using weighted node embeddings. Notice that due to this joint training, as the surrogate classifier learns to better mimic the original GNN, the node scoring module learns to produce higher scores for more important nodes.

![backward-pass]({{site.baseurl}}/material/2022/post_16/training.jpeg?raw=true){:width="620px"}

Once this training is completed using all the graphs to be explained, the explainer can directly prune out nodes with smaller scores. What is left after that is a subgraph that contributes the most towards the malware classification task. 

In our experiments we found that CFGExplainer is able to produce subgraphs (~20% original size) that indicate malicious patterns such as obfuscation tricks and code manipulations that would have been harder to manually identify by analyzing the complete malware graph. If you want to learn more about **CFGExplainer** please check our [paper](https://www.dinalherath.com/papers/2022dsn.pdf) and [code](https://github.com/dherath/CFGExplainer).

![results]({{site.baseurl}}/material/2022/post_16/results.jpeg?raw=true){:width="820px"}

##### So until next time,
##### Cheers!

**Prev: [Fooling AI-based System Log Anomaly Detection]({{site.baseurl}}/2021/lam/)**