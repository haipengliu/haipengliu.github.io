---
layout: post
title: "Introduction to CRF"
date: 2014-11-15 08:55:38 +0800
comments: true
categories: [CRF, Machine Learning]
---
Author: Haipeng Liu <A href="mailto:pliu1981@gmail.com">email to me</A></br>
keywords: CRF</br>

#Sequential labelling problem
 
**Conditional random** field is proposed to model the sequence data. The sequence data are the data or objects with a sequence structure.
For example, in Noun-Phrase (NP) chunking task, for a sentence, we want to provide correct phrasal labels for each word. The phrasal labels are B-NP for the beginning words of a noun-phrase, I-NP for the words inside a noun-phase and O for others. For instant, a labelled sentence in the CoNLL2000 dataset reads like this. 

> Chancellor/O of/O the/B-NP Exchequer/I-NP Nigel/B-NP Lawson/I-NP 's/B-NP restated/I-NP commitment/I-NP to/O a/B-NP firm/I-NP monetary/I-NP policy/I-NP has/O helped/O to/O prevent/O a/B-NP freefall/I-NP in/O sterling/B-NP over/O the/B-NP past/I-NP week/I-NP ./O

*CoNLL2000*

The CRF can automatically label the noun phrase character as the human does

#Model the sequence
To model the labeling process. We use $x$ to denote the labels and $z$ to denote the data. In our case $x$ is the sequence of noun phrase labels and $z$ is the sequence of words. $t$ is the sequence index. Also, $x$ is named hidden state variables, $z$ is named the observations. The task of CRF is to predict the state variables given the observations. That is to compute the probability:
   <!-- more -->   
$P(x|z)$, where $x = (x_1, x_2, ..., x_T)$ the labels, $z$ the data, $t\in[1, T]$ sequence index.
 
#Potential functions
With the theory of undirected Markov chain, the conditional probability of $x$ given $z$ is defined as the product of a serial potential functions. Where:</br>

$$P(x|z) = \frac{1}{Z(z)}\sum_{c}\psi_c(x_c, z)$$
$\psi_c(x_c, z)$ - potential function<\br>
$Z(z) = \sum_x\prod_c\psi_c(x_c, z)$ - partition function<\br>

 $\psi$ are positive functions known as potentials.</br>
 $Z(z)$ is the normalization constant known as the partition function, which guarantees the formula return a value in the range from zero to one. It’s the sum of the potentials but accounting for all the possible x values, which can be treated as the edge probabilities along side the $x$. </br>
 The number of potentials is denoted by $c$. Here in undirected Markov chain, $c$ stands for clique, which means different connections among nodes. In CRF, generally there are two kinds of connections, one is the current node connecting observation nodes, another is the nearby two nodes connecting observations nodes. They are corresponded to two kinds of potentials – **node potential** and **edge potential**.
 
>Two types of potentials</br>
node potential of label $x_t$ at time $t$

$$\begin{equation}\phi_t(x_t, z) = exp(\sum_k\omega_kf_k(x_t, z, t))\dots\end{equation}~Eq.(1)\dots~a~S\times{}T~matrix$$

The concept of potentials can be imagined as energies. Those local, nearby pieces of energies are used to compose the probability. The potentials refer to some quantities that tie the labels and the local data patterns at particular time together. In the simplest case which is often used in practice, potentials are exponential of sum of weighted features. There are usually two types of potential functions: node potential functions and edge potential functions, according to different clique styles they are connected. 

##Node Potential
The node potential phi describes the contribution of the current node and its connecting observations to the global model. The edge potential psi describes the contribution of two nearby labels and their connecting observations to the global model. The connections is modeled by feature functions. Where f is called a feature function, omega is the weight for a feature and K is the number of features. Feature functions connect the labels and the observed data. There may be S labels and T observations.