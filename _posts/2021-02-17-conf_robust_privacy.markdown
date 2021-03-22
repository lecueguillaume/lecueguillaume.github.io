---
layout: post
title:  Conference on robustness and privacy
comments: true
header-includes: |
    \usepackage{tikz,pgfplots}
    \usepackage{fancyhdr}
    \pagestyle{fancy}
    \fancyhead[CO,CE]{This is fancy}
    \fancyfoot[CO,CE]{So is this}
    \fancyfoot[LE,RO]{\thepage}
date:   2021-02-17
---

We are organizing a two days virtual conference on "robustness and privacy" on March 22 and March 23, 2021.   

The registration is free but mandatory; a Zoom link will be sent to all participants a day before the conference

[<center><font face="verdana" size='5' color='blue'> register here </font></center>](https://docs.google.com/forms/d/e/1FAIpQLSf_yZApHaZVZ791DXR-sAP--R_bnkeJ6EEKr_F0qNDrWFmUiw/viewform?vc=0&c=0&w=1&flr=0&usp=mail_form_link)




Each talk will be 25 minutes long followed by a 5 minutes dicussion for questions. The conference should start on Monday 22th of March and Tuesday 23rd of March at 16:30 up to 19h40 (Paris local time).


**Confirmed speakers:**



[<center><font face="verdana" size='5' color='red'> Marco Avella Medina </font></center>](https://sites.google.com/site/marcoavellamedina/home)
**Title: Differentially private inference via noisy optimization**

*Abstract:* We propose a general optimization-based framework for computing differentially private M-estimators and  a new method for the construction of differentially private confidence regions. Firstly, we show that robust statistics can be used in conjunction with noisy gradient descent and noisy Newton methods in order to obtain optimal private estimators with global linear or quadratic convergence, respectively. We establish global convergence guarantees, under both local strong convexity and self-concordance, showing that our private estimators converge with high probability to a neighborhood of the non-private M-estimators. The radius of this neighborhood is nearly optimal in the sense it corresponds to the statistical minimax cost of differential privacy up to a logarithmic term. Secondly, we tackle the problem of parametric inference by constructing differentially private estimators of the asymptotic variance of our private M-estimators. This naturally leads to the use of approximate pivotal statistics for the construction of confidence regions and hypothesis testing. We demonstrate the effectiveness of a bias correction that leads to enhanced small-sample empirical performance in simulations. We illustrate the benefits of our methods with synthetic numerical examples and real data.

This is joint work with Casey Bradshaw and Po-Ling Loh.

Link to [paper](https://drive.google.com/file/d/12mY6FaDX1xxLOdOT2OiI3oJ-ogcCl6Y1/view)

[<center><font face="verdana" size='5' color='red'> Tom Berrett </font></center>](https://thomasberrett.github.io) 

**Title: Locally private non-asymptotic testing of discrete distributions is faster using interactive mechanisms**



*abstract:* In this talk I will present recent work on goodness-of-fit testing under local differential privacy constraints. There are two broad classes of locally private procedures: simple non-interactive procedures and interactive procedures where communication is allowed between individual data holders. One of the main conclusions of our work is that the minimax separation rates are significantly faster using interactive mechanisms.
 
We find the minimax separation rates for testing multinomial or more general discrete distributions. Our upper bounds are found by constructing efficient randomized algorithms and test procedures, in both the case where only non-interactive privacy mechanisms are allowed and also in the case where all sequentially interactive privacy mechanisms are allowed, and establish a gap between the rates. We prove general information theoretical bounds that allow us to establish the optimality of our algorithms among all pairs of privacy mechanisms and test procedures, in most usual cases. Considered examples include testing uniform, polynomially and exponentially decreasing distributions.

link to  [paper](https://papers.nips.cc/paper/2020/hash/20b02dc95171540bc52912baf3aa709d-Abstract.html)


[<center><font face="verdana" size='5' color='red'> Clément Canonne </font></center>](https://ccanonne.github.io)
**Title: Lower bounds for high-dimensional estimation under "local" information constraints**

*abstract:* The focus of this talk is distributed parameter estimation using interactive protocols subject to "local information constraints."
Those constraints include, among others local differential privacy (LDP), communication constraints, and restricted measurements.

I'll cover recent work which provides a general framework which lets us obtain tight lower bounds for both estimation and testing of discrete distributions. I'll then discuss how to extend this framework to other parametric families, including mean estimation for product distributions over the hypercube and high-dimensional Gaussians.

Based on joint works with Jayadev Acharya, Yuhan Liu, Ziteng Sun and Himanshu Tyagi.

Links to [paper 1](https://arxiv.org/abs/2007.10976) and [paper 2](https://arxiv.org/abs/2010.06562)


[<center><font face="verdana" size='5' color='red'> Olivier Catoni </font></center>](http://ocatoni.perso.math.cnrs.fr)
**Means and $k$-means: dimension free  PAC-Bayesian bounds for some robust estimators**

*[abstract:](/assets/abstract_olivier_catoni.pdf)* We will show, through results obtained in collaboratiton with Ilaria Giulini and Gautier Appert, how PAC-Bayesian  bounds can be used as an alternative to other methods to prove concentration inequalities and complexity bounds. We will take the example of the robust estimation of the mean of a random vector. We will then discuss the problem of vector quantization according to a robust modification of the $k$-means loss function.

Links to [paper 1](https://arxiv.org/abs/2101.05728), [paper 2](https://projecteuclid.org/journals/annales-de-linstitut-henri-poincare-probabilites-et-statistiques/volume-48/issue-4/Challenging-the-empirical-mean-and-empirical-variance--A-deviation/10.1214/11-AIHP454.full), [paper 3](https://bguedj.github.io/nips2017/pdf/PAC-Bayes_2017_paper_1.pdf) and [paper 4](https://arxiv.org/abs/1712.02747).

[<center><font face="verdana" size='5' color='red'> Yeshwanth Cherapanamjeri </font></center>](https://yeshwanth94.github.io) 
**Title: Optimal Mean Estimation without a Variance**

*Abstract:* Estimating the mean of a distribution from i.i.d samples is a fundamental statistical task. In this talk, we will focus on the high dimensional setting where we will design estimators achieving optimal recovery guarantees in terms of all relevant parameters. While optimal one dimensional estimators have been known since the 80s (Nemirovskii and Yudin '83), optimal estimators in high dimensions have only been discovered recently beginning with the seminal work of Lugosi and Mendelson in 2017 and subsequent work has led to computationally efficient variants of these estimators (Hopkins 2018). We will discuss statistical and computational extensions of these results by developing optimal estimators for settings where the data distribution only obeys a finite fractional moment condition as opposed to the existence of a second moment as assumed previously. 

Joint work with Peter Bartlett, Nicolas Flammarion, Michael I. Jordan and Nilesh Tripuraneni.

The talk will be based on the following papers: [paper 1](https://arxiv.org/abs/2011.12433) and [paper 2](https://arxiv.org/abs/1902.01998).


[<center><font face="verdana" size='5' color='red'> Jules Depersin </font></center>](https://julesdepersin.github.io) 
**Title: Using VC-dimension in robust estimation**


*abstract:* Median-of-means (MOM) based procedures provide non-asymptotic and strong deviation bounds even when data are heavy-tailed and/or corrupted. We will try to explain how those procedures can easily be adapted to a number of different statistical problems, and we will give the general ways to bound the excess risk for MOM estimators, with an emphasis on the different notions of statistical complexity (VC dimension, Rademacher complexity) that can be used to do so. We will see that each classical notion of complexity is suboptimal in its own way, leaving open the question of the optimal way to measure the statistical complexity of robust estimation problems.

Link to [paper](https://arxiv.org/abs/2004.11734)

[<center><font face="verdana" size='5' color='red'> John Duchi </font></center>](https://web.stanford.edu/~jduchi/) 
**Title: Near Instance-Optimality in Differential Privacy**

*Abstract:* We develop two notions of instance optimality in differential privacy, inspired by classical statistical theory: one by defining a local minimax risk and the other by considering unbiased mechanisms and analogizing the Cramer-Rao bound, and we show that the local modulus of continuity of the estimand of interest completely determines these quantities. We also develop a complementary collection mechanisms, which we term the inverse sensitivity mechanisms, which are instance optimal (or nearly instance optimal) for a large class of estimands. Moreover, these mechanisms uniformly outperform the smooth sensitivity framework on each instance for several function classes of interest, including real-valued continuous functions. We carefully present two instantiations of the mechanisms for median and robust regression estimation with corresponding experiments.

Based on joint work with Hilal Asi

Linto [paper](https://arxiv.org/abs/2005.10630)

[<center><font face="verdana" size='5' color='red'> Chao Gao </font></center>](https://www.stat.uchicago.edu/~chaogao/) 
**Title: Robust Regression with Contamination**

*abstract:* We study regression with contaminated observations. We will discuss different results depending on whether both the responses and the covariates are contaminated or only the responses are contaminated. General minimax rates are derived based on regression depth functions when both the responses and the covariates are contaminated. The result implies consistency is possible only if the contamination proportion is vanishing. In comparison, we show that when the covariates are clean, consistent robust regression is actually possible even when the contamination proportion approaches one. A near-optimal procedure in this case is the simple median regression. Applications of the second setting in model repair problems will also be discussed.

[<center><font face="verdana" size='5' color='red'> Sam Hopkins </font></center>](https://www.samuelbhopkins.com) 
**Title: Robustly Learning any Clusterable Mixture of Gaussians**

*Abstract:* We study the efficient learnability of high-dimensional Gaussian mixtures in the outlier-robust setting, where a small constant fraction of the data is adversarially corrupted. We resolve the polynomial learnability of this problem when the components are pairwise separated in total variation distance. Specifically, we provide an algorithm that, for any constant number of components \\( k \\), runs in polynomial time and learns the components of an \\( \epsilon \\)-corrupted \\( k \\)-mixture within information theoretically near-optimal error of \\( O(\epsilon) \\), under the assumption that the overlap between any pair of components \\( Pi,Pj \\) (i.e., the quantity \\( 1−TV(Pi,Pj)\\)) is bounded by poly(\\( \epsilon \\))). 

Our separation condition is the qualitatively weakest assumption under which accurate clustering of the samples is possible. In particular, it allows for components with arbitrary covariances and for components with identical means, as long as their covariances differ sufficiently. Ours is the first polynomial time algorithm for this problem, even for \\( k=2 \\). 

Our algorithm follows the Sum-of-Squares based proofs to algorithms approach. Our main technical contribution is a new robust identifiability proof of clusters from a Gaussian mixture, which can be captured by the constant-degree Sum of Squares proof system. The key ingredients of this proof are a novel use of SoS-certifiable anti-concentration and a new characterization of pairs of Gaussians with small (dimension-independent) overlap in terms of their parameter distance.


[<center><font face="verdana" size='5' color='red'> Gautam Kamath </font></center>](http://www.gautamkamath.com/) 
**Title: Differentially Private Mean and Covariance Estimation**

*Abstract:* We cover recent progress in minimax rates for differentially private parameter estimation. As a canonical example, how much data do we need to estimate the parameters of a multivariate Gaussian distribution? A particular focus will be placed on qualitative differences with the non-private setting.

Links to [paper 1](https://arxiv.org/abs/1805.00216) and [paper 2](https://arxiv.org/abs/2002.09464)

[<center><font face="verdana" size='5' color='red'> Pavlo Mozharovskyi </font></center>](https://perso.telecom-paristech.fr/mozharovskyi/)
**Title: Approximate computation of projection depths**

*Abstract:* Data depth is a concept in multivariate statistics that measures the centrality of a point in a given data cloud in the Euclidean space. If the depth of a point can be represented as the minimum of the depths with respect to all one-dimensional projections of the data, then the depth satisfies the so-called projection property. Such depths form an important class that includes many of the depths that have been proposed in literature. For depths that satisfy the projection property an approximate algorithm can easily be constructed since taking the minimum of the depths with respect to only a finite number of one-dimensional projections yields an upper bound for the depth with respect to the multivariate data. Such an algorithm is particularly useful if no exact algorithm exists or if the exact algorithm has a high computational complexity, as is the case with the halfspace depth or the projection depth. To compute these depths in high dimensions, the use of an approximate algorithm with better complexity is surely preferable. Instead of focusing on a single method we provide a comprehensive and fair comparison of several methods, both already described in the literature and original.

Link to [paper](https://arxiv.org/abs/2007.08016)

[<center><font face="verdana" size='5' color='red'> Weijie Su </font></center>](https://statistics.wharton.upenn.edu/profile/suw/) 
**Title: A Central Limit Theorem for Differentially Private Query Answering**

*Abstract:* Perhaps the single most important use case for differential privacy is to privately answer numerical queries, which is usually achieved by adding noise to the answer vector. The central question is, therefore, to understand which noise distribution optimizes the privacy-accuracy trade-off, especially when the dimension of the answer vector is high. Accordingly, extensive literature has been dedicated to the question and the upper and lower bounds have been matched up to constant factors. In this talk, we take a novel approach to address this important optimality question. We first demonstrate an intriguing central limit theorem phenomenon in the high-dimensional regime. More precisely, we prove that a mechanism is approximately Gaussian differentially private if the added noise satisfies certain conditions. In particular, densities proportional to \\(\exp(-\|x\|_p^\alpha)\\), where \\(\|x\|_p\\) is the standard \\(\ell_p\\)-norm, satisfies the conditions. Taking this perspective, we make use of the Cramer--Rao inequality and show an uncertainty principle style result: the product of privacy parameter and the \\(\ell_2\\)-loss of the mechanism is lower bounded by the dimension. Furthermore, the Gaussian mechanism achieves the constant-sharp optimal privacy-accuracy trade-off among all such noises. Our findings are corroborated by numerical experiments. This is joint work with Jinshuo Dong and Linjun Zhang.

Link to [paper](https://arxiv.org/pdf/2103.08721.pdf)




<!-- [<center><font face="verdana" size='5' color='red'>  </font></center>]() 
 -->

<!-- Sabato, Gao, Minsker, --> 

<!-- Daniel Kane --> 

<!-- Amandine Dubois -->

**Schedule (Paris local time)**

<center>

<table>
  <tr>
    <th>   </th>
    <th style="background-color: yellow">Monday 22 March</th>
    <th style="background-color: red">Tuesday 23 March</th>
  </tr>
  <tr>
    <td>16:30 -- 17:00</td>
    <td style="background-color: yellow">Olivier Catoni</td>
    <th style="background-color: red">Weijie Su</th>
  </tr>
  <tr>
    <td>17:00 -- 17:30</td>
    <td style="background-color: yellow">Samuel Hopkins</td>
    <th style="background-color: red">Gautam Kamath </th>
  </tr>
    <tr>
    <td>17:30 -- 18:00</td>
    <td style="background-color: yellow"> Pavlo Mozharovskyi</td>
    <th style="background-color: red">Clément Canonne </th>
  </tr>
    <tr>
    <td>18:00 -- 18:10</td>
    <td style="background-color: yellow">BREAK </td>
    <th style="background-color: red"> BREAK  </th>
  </tr>
    <tr>
    <td>18:10 -- 18:40</td>
    <td style="background-color: yellow">Tom Berrett </td>
    <th style="background-color: red"> Yeshwanth Cherapanamjeri  </th>
  </tr>
    <tr>
    <td>18:40 -- 19:10</td>
    <td style="background-color: yellow">Marco Avella Medina</td>
    <th style="background-color: red"> Jules Depersin  </th>
  </tr>
    <tr>
    <td>19:10 -- 19:40</td>
    <td style="background-color: yellow">John Duchi</td>
    <th style="background-color: red"> Chao Gao  </th>
  </tr>
</table>


</center>



    

**Support**
The conference is suported by the mathematical institute of CNRS and the Médiamétrie Chair. 

**Some words about the conference:**

**Robustness** has been studied a lot in statistics since the seminal work of Huber. Many algorithms have also been designed in Machine Learning. However, this subject has witnessed an important renew  during the last 10 years both in the statistical and computer science communities. It involves statistics, optimization, probability and machine learning as mathematical domains. 

In the meantime, **privacy** has received a lot of attention in the Computer science community because it is a central issue for the security of many sensitive data in finance, economics, administration and, more basically, for keeping customers' trust in trading. It seems however possible to randomize data in order to ensure a controlled amount of privacy of the individuals while still being able to learn some patterns out of it: this is the cornerstone of privacy. Only  recently, statisticians started to analyze privacy mechanisms. In particular, they discovered several interesting common features between robustness issues and privacy. That is the main motivation on our side to organize a joint conference simultaneously on the two subjects. 

**Organization commitee:**
Cristina Butucea, Victor-Emmanuel Brunel, Nicolas Chopin,  Arnak Dalalyan, Guillaume Lecué, Matthieu Lerasle, Vianney Perchet and Alexandre Tsybakov.

**Info contact** You can email [me](https://lecueguillaume.github.io/about/) for more information.




 