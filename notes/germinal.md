---
title: Germinal
created: '2020-04-05T19:41:03.576Z'
modified: '2020-04-10T17:44:11.139Z'
---

# Germinal
Note: This page is a work-in-progress.

## Overview – What Is This
This project is pedagogical. It's the record of my attempt to develop a system which solves a problem I have. The value of this work does not come from the accuracy or precision of the system itself – although these will hopefully reach an acceptable state – but from the conceptualization and analogy which its creation motivates. This is a record of the process of developing a functional system, starting from a set of techniques and an existing system, reconceptualizing the system on some level (for example the structure of the system itself, or the structure or function of the components, or the ways in which the components interact) in a way which motivates a modification to the system, or new method in which to leverage the system, which is then implemented in a functional way in code. The result is a program which encodes this reconceptualization – in this way, "the buck stops" with the code.

### Motivations
From the individual's perspective, the amount of written knowledge now free – in all senses of the word – and openly available is functionally unlimited. In a signal-rich environment creation is synthesis; synthesis of ideas from disparate and varied sources. Different texts, works produced by practitioners from different fields and different institutions, with different motivations and perspectives – fundamentally, the creation of value is identified with the synthesis of all of this into novel work which builds on it and sits atop it. 

Of course, this signal is buried under mountains of noise – we need methods to separate the two. Such methods are known as [information retrieval systems](https://en.wikipedia.org/wiki/Information_retrieval). 

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
- [Information Retrieval](https://en.wikipedia.org/wiki/Information_retrieval)
- [Pre-trained Models for Natural Language Processing: A Survey](https://arxiv.org/pdf/2003.08271.pdf)
- [Logistic Regression in Sci-kit Learn](https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression)
