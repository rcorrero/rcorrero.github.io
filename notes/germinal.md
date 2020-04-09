---
title: Germinal
created: '2020-04-05T19:41:03.576Z'
modified: '2020-04-09T21:10:03.785Z'
---

# Germinal

## Overview
### What is this
This project is pedagogical. It's the record of my attempt to develop a system which solves a problem I have. Don't be fooled by the high-minded language with which I present my motivations: this is an amature's attempt to design an information retrieval system. There are obviously many existing tools developed by teams of professionals, and it is almost certain that, whatever your information retrieval needs, these tools will be much more useful to you than anything I may hope to create. The value of this work does not come from the accuracy or precision of the system itself – although these will hopefully reach an acceptable state – but from the conceptualization and analogy which they motivate. This is a record of the process of developing a functional system, starting from a set of techniques and an existing system, reconceptualizing the system on some level (for example the structure of the system itself, or the structure or function of the components, or the ways in which the components interact) in a way which motivates a modification to the system, or new method in which to leverage the system, which is then implemented in a functional way in code. The result is a program which encodes this reconceptualization – in this way, "the buck stops" with the code.

### Motivations
From the individual's perspective, the amount of knowledge now free – in all senses of the word – and openly available in functionally unlimited. In a signal-rich environment creation is synthesis; synthesis of ideas from disparate and varied sources. Different texts, works produced by practitioners from different fields and different institutions, with different motivations and perspectives – fundamentally, the creation of value is identified with the synthesis of all of this into novel work which builds on it and sits atop it. 

This is a normative value judgement with respect to knowledge creation. It's useful in that it motivates an analysis of the way in which individuals interact with massive, functionally infinite, knowledges reserves presented by repositories, databases, and the federal knowledge hierarchy of the internet itself. 

- Describe the hierarchy implicit in keyword search methods

- Describe why this hierarchy is at odds with the view above presented, that synthesis yields something which is greater than the sum of its parts and that the domain of knowledge, broadly construed, must be understood to be continuous, unconstrained by the arbitrary boundaries which are imposed by the economic, sociopolitical, and practical forces which dictate the structure and function of the knowledge production machine. This motivates the development of methods which encourage the individual to dispense with these notions, which elevate synthesis and serendipity above accordance with the taxonomy imposed on knowledge. Methods which approximate the continuous surface presented by the sum total of human knowledge and allow the user to efficiently navigate it.

- Attempt to do the above: Germinal flattens the information hierarchy, replacing the taxonomic structure with the embedding space, in which the complex relationships between texts are encoded in a flat way. This is facilitated through the use of embedding and decomposition methods.

## Abstractions and Implementation
The problem of text recommendation may be modeled as a [non-contextual bandit problem](https://repository.upenn.edu/cgi/viewcontent.cgi?article=1501&context=statistics_papers).

### Pedagogical Iteration 1
- Learning Objectives
 1. Design and implement basic non-contextual linear bandit algorithm which uses some annealing schedule to fit parameters.
 2. Implement preprocessing steps
  - Tfidf conversion
  - Decomposition and transformation into $k$-dimensional topic space using NMF
 as a pipeline to create topic space and transform texts.
 3. Design basic observation ui which
  - Prompts the user for seed text(s)
  - Responds with (estimated) most relevant text
  - Asks the user whether the text is relevant or not (Respond `[y]es` if so and `[n]o` otherwise)
  - If `yes`, $r_t = 1$; $r_t = -1$ otherwise. The code for this is called within the `while` loop of the NLB algorithm, and after receiving reward $r_t$ the algorithm updates $\hat\mu_t$ as follows:
  $$\hat\mu_t += r_t \cdot x_t$$
  where $x_t$ is the embedding in topic space of the text presented at $t$.

#### _ConfidenceBall_ Iterative SVM Model
The [ConfidenceBall](https://repository.upenn.edu/cgi/viewcontent.cgi?article=1501&context=statistics_papers) model presented by Dani et. al. is similar to the method we will develop in that it makes a greedy selection at each round and then updates its estimate of some parameter $\hat\mu_t$ based on the observed reward. Our method is simplier because we have a set of discrete vectors (embeddings of the texts in the corpus) from which to sample.

## Avenues of Inquiry
- Develop a standard python framework for tasks which use "shallow" models such as ordinary least squares or logistic regression with two types of predictors:
  - High-dimensional features produced by deep neural models
  - Low-dimensional features of relevance to the particular problem
- Create a method to fit the parameters of the shallow model using user-generated samples.

## References
- [Stochastic Linear Optimization Under Bandit
Feedback](https://repository.upenn.edu/cgi/viewcontent.cgi?article=1501&context=statistics_papers)
- [A Tutorial on Thompson Sampling](https://web.stanford.edu/~bvr/pubs/TS_Tutorial.pdf)
- [Using Confidence Bounds for
Exploitation-Exploration Trade-offs](http://www.jmlr.org/papers/volume3/auer02a/auer02a.pdf)
- [Finite-Time Analysis of Kernelised Contextual Bandits](https://arxiv.org/pdf/1309.6869.pdf)
- [Reinforcement Learning](https://en.wikipedia.org/wiki/Reinforcement_learning)
- [node2vec: Scalable Feature Learning for Networks](https://arxiv.org/pdf/1607.00653.pdf)
