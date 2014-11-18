---
layout: post
title: "Introduction to CRF(2)"
date: 2014-11-18 17:27:47 +0800
comments: true
categories: [CRF, Machine Learning]
---
Author: Haipeng Liu <A href="mailto:pliu1981@gmail.com">email to me</A></br>
keywords: CRF</br>

#Feature Engineering

Features are perhaps the most important elements of the statistic model. Good feature engineering can often increase the labelling accuracy very significantly.  

A feature function associates the labels and the local data patterns. The node feature take into account the current label $x_t$ and an element of data pattern $g_m[z, t]$. where $\delta[x_t, s]$ is the indicator function. It returns 1 if label of $x$ at $t$ is the label $s$ and 0 otherwise.

The data pattern function $g_m(z, t)$ takes care of the raw data and returns a (real or binary) value. For example, in noun-phrase chunking, we may have a feature $g$ the 100th.  That is, the 100th data feature receives value of 1 at current time $t$ of $10$ if the previous word is *today*.

<--! more -->