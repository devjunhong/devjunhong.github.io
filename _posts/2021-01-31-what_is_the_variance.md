---
title: "What is the variance in machine learning?"
excerpt: "Hard to find a practical definition of variance"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/31/bias_and_variance.png
#   image: /assets/images/2021/01/24/openface_og_updated.png
#   caption: "Photo by me"
  og_image: /assets/images/2021/01/31/bias_and_variance.png
layout: single
# classes: wide

categories:
    - Machine Learning
tags:
    - Bias
    - Variance
last_modified_at: 2021-01-31T08:06:00-05:00
---

# Intro
![bias and variance](/assets/images/2021/01/31/bias_and_variance.png)
How can we tell a model is over-fitting or under-fitting? We can use bias and variance. Can you also describe the objective term of bias and variance? For example, can you fill in what is "something" in these statements; the bias of "something" or variance of "something". In this short post, I'm trying to explain this and some of the trials to overcome those barriers. 

# Bias 
Bias is a difference between the prediction value and the ground truth.

# Variance
Variance measures the variability of the model prediction if we would re-train the same model multiple times on different subsets of the data. 

[https://datascience.stackexchange.com/a/42437](https://datascience.stackexchange.com/a/42437)

The variance term is hard to get a practical idea. I found several definitions, but I can't grasp what the variance means. So that, I want to keep the definition as short as possible I can remember. 

# Over-fitting 
A model memorizes the train data set so that it fluctuates a lot when there are unseen data. To overcome, we can try; 

* Regularization 
* Dropout 
* Early Stopping 
* Reduce the complexity of the model

# Under-fitting 
A model even doesn't fit on the training set. To combat with, we can follow;

* Increase the model size and parameters 
* Run more steps to fit well 
* Get more training data

# Outro 
In this short post, I want to explain what variance means in machine learning. I faced definitions, but I had no idea about how can we calculate.