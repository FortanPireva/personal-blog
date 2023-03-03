---
title: 'Machine Learning Basics'
date: '2023-01-03'
image: 'https://miro.medium.com/max/1400/0*fsmYfkJYo_n_Uhph'
tags: ['machine_learning', 'ai']
---

The very basic idea of machine learning is the learning algorithm. But what exactly is a learning algorithm ?

![](https://miro.medium.com/max/1400/0*fsmYfkJYo_n_Uhph)

A Machine Learning Algorithm is an algorithm that is able to learn from data. That is a rather abstract and basic definition but sufficient enough.

> ” A computer program it said to learn from experience E, with respect to some task T, given performance P, if its performance at task T, as measured by P, improves with experience E”.

The learning part is otherwise described as a means of attaining the ability to perform the task.

There are quite some different categories of tasks:

1.  Classification ( e.g. object recognition)
2.  Classification with missing inputs
3.  Regression ( a linear function which take an input of dimensionality N and outputs 1 dimensional value)
4.  Transcription ( e.g optical character recognition, speech recognition)
5.  Machine Translation
6.  Synthesis and analysis ( texture generation in computer games)
7.  ….

In terms of experience E, Machine learning algorithms are divided into 2 major groups, **supervised** and **unsupervised** learning algorithms. The former one, learn from given input data in forms of features, which are pairs of labels, and target. The accuracy of the learning algorithm is thus calculated as the percentage of wrong predictions made against the actual target data.

For unsupervised learning algorithms the learning algorithm experiences many features, and tries to learn useful properties of the structure of dataset.

**Capacity, Overfitting, and Underfitting**

The ultimate goal of a machine learning algorithm is to reduce the generalization error, also known as test error as much as possible. This value represents the expected value of the error in new input.

**Underfitting** — is the inability of the model to have the error in the training set be sufficiently low.

**Overfitting** — occurs when there is large gap between training error and testing error.

Overfitting and underfitting can be controlled by varying the model capacity.

**The** **capacity** of the ML model is the ability to fit in various kind of functions, which is controlled by choosing the hypothesis space. This hypothesis space is the set of functions that the algorithm is allowed to select as being the solution.
