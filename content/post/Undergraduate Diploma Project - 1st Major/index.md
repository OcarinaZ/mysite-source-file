---
title: Stock Price Prediction Based On Hidden Markov Model
description: Undergraduate Diploma Project - 1st Major
date: 2021-06-21
slug: diploma1st
image: Cover.jpg
categories:
    - Past Projects
tags:
    - Hidden Markov Model
    - Index Price Prediction
    - Maximum a Posteriori
---

Recently, Hidden Markov Model (HMM) has achieved certain application and development in stock market price and trend prediction. Existing HMM-based price prediction methods mainly predict the closing price of the next day by either (1) likelihood: finding price sequences in historical data which have similar pattern with current data; (2) MAP: discretizing the range of observable variable to form thousands of alternatives, from which the one with highest MAP will be selected as price prediction. The two approaches above face the problems of excessive computational costs or lacking double-check of posterior probability, where still remains possibility of optimization. Thus, this article put forward two new methods of price prediction, namely, likelihood-MAP approach and likelihood-posterior-probability-weighted approach, based on the analysis of traditional likelihood and MAP approaches, aiming at improving prediction accuracy as well as reducing computational burden in time. These two new methods correspond to two different optimization approaches, namely (1) completing a MAP double-check using alternatives (normally only dozens) drawn from likelihood method to obtain the prediction (likelihood-MAP approach); (2) using posterior probability as the weight of alternatives to get a weighted price as prediction.   

As for empirical aspect, the research has used CSI 300 Index as data source to construct 105 technical factor groups as the observable variables of HMM, with different window length and different prediction length have also been taken into consideration as robustness test of the new prediction approaches. The empirical results show that the new approaches in this article have better performances than traditional ones, which is in accordance with the expectations of this research, and may be able to provide references for further trading strategy construction.


