---
title: Spoken Digit-Pair Recognition
description: ECE 5420 - Fundamentals of Machine Learning Kaggle Competition Project
date: 2021-12-06
slug: ece5420
image: Cover.jpeg
categories:
    - Past Projects
tags:
    - Machine Learning
    - Spoken Digit-Pair Recognition
    - Logistic Regression
---

## Overview
In the project, mainly 4 kinds of machine learning methods (Naïve Bayesian, Logistic Regression, Support Vector Machine and Decision Tree) are tested, along with the additional processing with the ‘missing’ label ’43’ in training set. In addition, time efficiency of all methods is also recorded. As a result, the Logistic Regression has the highest prediction accuracy (92.6%) with relatively short time consumed. 

## Work Details

As mentioned in the overview, the most challenging part of dealing with the spoken digit-pair data set is that label ‘43’ is not included in the training set, but it appears in the testing set. Thus, firstly all four ML methods are tried on the training data to find the ones that have lowest estimation error, and then different kinds of algorithms are used to figure out the ‘43’ label in testing data set based on the selected ML method.

As for implementing ML methods on training data, considering about the space it needs to take for reading and analyzing all 90000 training data, the project used batching to save space while maintaining the effect of training on large data set. That is: (1) randomly select 10000 data from the whole training data set each time and separate it into training and testing set; (2) train/update the machine learning model on this new smaller data set; (3) repeat (1) and (2) and update the original machine learning model in each batch (9 batches in all). As a result, the logistic regression and SVC model achieved the highest accuracy (about 91%). A bagging-like process that selected the most commonly appearing labels in 18 batches (5000 data in each loop) for each testing data was also tried, but its result was not as good as not doing extra manipulation. 

Based on the basic ML model selected above, when it comes to dealing with label ‘43’ that doesn’t appear in the training set, 3 algorithms were tried: 

* Algorithm 1: randomly swap the order of the two labels of one data in order to make the combination of ‘43’ possible, split the labels of all training data (after the swap) into two label series, and train the machine learning model on each series separately. Finally, combine the single label predictions from two models into the series of two labels for one testing data.  

* Algorithm 2: make a copy of training data, split the 2-digit label into two 1-digit labels for each training data and distribute the 1-digit labels to training data (e.g. (X,’32’) -> (X,’3’), (X.’2’)). Then train the machine learning model on this new training set and select the top 2 labels with the largest probability.  

* Algorithm 3: as ‘43’ doesn’t exist in training set, it might be possible to find a proper threshold on the probability so that we can distinguish the data in testing set whose true label is ‘43’ but mistakenly classified as other labels.

As a result, Algorithm 1 would produce too many labels with the same number such as ‘11’ or ‘22’, which may be explained by the fact that when trained separately, some of the data will be treated as noise, and with only one label given to actually two digit’s wave data, true data itself may be treated as noise and thus leads to the repeated label in 2-digit labels.
As a solution to this problem, Algorithm 2 is designed. This algorithm solves both the problem of missing ‘43’ and misrecognizing noise by including both labels separately in the training set. Logistic regression based on this algorithm reaches the accuracy of 92.6%.
Algorithm 3 seems to work but actually it is difficult to find a threshold. The testing data with true label ‘43’ still have quite high prediction probability on other labels (e.g. 90% for label ‘41’ when true label is ‘43’).

Finally, Algorithm 2 is chosen, and further research about other more complicated models such as HMM or CNN to deal with the ‘unobservable’ recognizing process and figure out ‘43’.
