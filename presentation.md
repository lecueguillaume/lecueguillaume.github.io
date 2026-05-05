---
marp: true
theme: gradient
class: blue
paginate: false
math: mathjax

---

<!-- _class: cover -->
# Structural parameters estimation in multi-partite networks.

Lucas Resende, **Guillaume Lecué**, Lionel Wilner,  Philippe Choné 

<div style="display: none;">

$$\newcommand{\cC}{\mathcal{C}} \newcommand{\cN}{\mathcal{N}} \newcommand{\cO}{\mathcal{O}} \newcommand{\bR}{\mathbb{R}} \newcommand{\bV}{\mathbb{V}}\newcommand{\bE}{\mathbb{E}} \newcommand{\bP}{\mathbb{P}}$$
</div>

---
### The Graph4Health project (ENSAE, ESSEC, INSERM, CASD)

Some of our aims:

1. understand the **impact of medical deserts** on health outcomes
2. construct tools to **evaluate health policy**
3. construct a **recommendation system** to help 'Médecin traitant' to recommend specialists, medical procedures, medicines, etc. to patients
4. prediction tools at the patient level: 'predictive medicine'

Based on the <span style="color: red;">SNDS database</span> (système national de santé).

---
### The SNDS database


The SNDS collects and stores health data from various sources:
1. public health agency (CNAM): <span style="color: blue;">SNIIRAM</span> from <span style="color: red;">'carte vitale'</span>  (système national d’information interrégimes de l’Assurance Maladie) (1998)
2. hospitals: <span style="color: blue;">PMSI</span> programme de médicalisation des systèmes d’information 
3. INSERM's databases on medical causes of death: <span style="color: blue;">CépiDc</span>  (Centre d’épidémiologie sur les causes médicales de décès, depuis 2017)
4. disability data: <span style="color: blue;"> MDPH and CNSA</span>  (2018) (maisons départementales des personnes handicapées and  Caisse nationale de solidarité pour l’autonomie, 2018)
5. a sample of data from <span style="color: blue;"> complementary health insurance</span> (2019) 


**One of the largest health database over $66$ millions of French peoples since 1998.** 

---
### The SNDS database
The purpose of the SNDS is to make these data available for <span style="color: blue;"> studies, research or evaluation</span>  contributing to one of the following purposes:

1. information on health;
2. implementation of public health policies;
3. knowledge of health expenditure;
4. informing professionals and institutions about their activities;
5. innovation in the fields of health and medico-social care;
6. surveillance, monitoring and health security.

---
### Accessing the SNDS

Since April 2017, any person or structure, public or private, for-profit or not-for-profit, can access SNDS data with the <span style="color: blue;"> authorization of the Cnil </span>, in order to carry out a study, research or evaluation of public interest.

Access to and use of SNDS data can only be made under conditions that respect the <span style="color: blue;"> SNDS security guidelines </span>, aimed at guaranteeing the confidentiality and integrity of the data and the traceability of access and other processing.

<br>

<div class="block">
  <div class="block-title">Graph4Health's dataset</div>
  <div class="block-content">
    We have been given access to 11 years of SNDS (2012--2022). So far we have data from 2016 to 2019 (**50 TB** of data).
  </div>
</div>

---
### Our aim in this presentation

<span style="color: blue;"> Set of questions 1 (structural / homophily parameters estimation):</span>
1. What is the impact of <u>distance</u> on our visits to doctors?
2. Do <u>women (resp. men)</u> visit more female (resp. male) doctors?
3. Do <u>young (resp. old)</u> people visit more often young (resp. old) doctors?

Based on **Cross-section data**: look at all consults in 2016.

<span style="color: blue;"> Set of question 2 (causality):</span>
1. what is the causal effect of a policy reform in May 2017 (Sector~1 GPs' fees have increased by $8.7\%$) on spatial accessibility to health care in France?

Based on **longitudinal data**: all consults from 2016 to 2018.

---
###  Cross-section data from year 2016

<div align="center">
  <img src="bipartite_graph_weights.svg" width="45%" />
</div>

---
### Statistical modelling: Poisson regression with fixed effects

<style scoped>
.split-screen {
    display: flex;
    align-items: center; /* Centers the math vertically with the image */
    justify-content: space-between;
}
.left-side {
    width: 50%;
}
.right-side {
    width: 69%;
}
</style>

<div class="split-screen">

<div class="left-side">

<img src="bipartite_graph_with_fixed_effects.svg" width="90%" />

</div>

<div class="right-side">

**The Model:** Edges' weight are independent and distributed according to (patient $i$ and doctor $j$)
$$Y_{ij} \sim Poisson(\lambda_{ij})$$
where:
$$\lambda_{ij} = \exp(\alpha_i + \delta_j + <X_{ij}, \beta>)$$

1. $\alpha_i$ and $\delta_j$ are the fixed effects (incidental parameters)
2. $\beta$ is the structural parameter
3. $X_{ij}$ a vector of features of the dyads $(i,j)$ (distance, same sex, same age bin, etc.)
</div>

</div>

---
### Maximum likelihood estimation (1/2)
**Our aim:** estimate $\beta$, the structural parameter. But there are incidental parameters of no interest = nuisance parameters...many of them...

**First approach = MLE**

<u>Step 1:</u> The probability density function under $\mathbb{P}_{(\beta, (\alpha_i)_i, (\delta_j)_j)}$ is 
$$
\begin{align}
f_{(\beta, (\alpha_i), (\delta_j))}: y \in \mathbb{N}^{PD} & \to  \mathbb{P}_{(\beta, (\alpha_i), (\delta_j))}[Y=y]\\ 
& = \prod_{i,j} \mathbb{P}_{(\beta, (\alpha_i), (\delta_j))}[Y_{ij}=y_{ij}] = \prod_{i,j} \frac{\lambda_{ij}^{y_{ij}}}{y_{ij}!}\exp(-\lambda_{ij})
\end{align}
$$

<u>Step 2:</u> the log-likelihood function is
$$
\mathcal{L}(\beta, (\alpha_i), (\delta_j)) = \log f_{(\beta, (\alpha_i), (\delta_j))} (Y)
$$ 

---
### Maximum likelihood estimation (2/2)
<u>Step 3:</u> The MLE $(\hat \beta, (\hat \alpha_i), (\hat\delta_j))$ maximizes

$$(\beta, (\alpha_i), (\delta_j)) \to \sum_{ij} Y_{ij}(\alpha_i + \delta_j + <X_{ij}, \beta>) - \exp(\alpha_i + \delta_j + <X_{ij}, \beta>).$$

Hence, to estimate $\beta$ (that is less than $10$ real numbers in general) we end up estimating $70$ millions coefficients!

<br>

>The impact of the incidental parameters (ie $\hat \alpha_i$'s and $\hat\delta_j$'s) on the estimation quality of $\hat\beta$ is known as the <span style="color: blue;"> Incidental Parameter Problem = IPP</span> (NS '48)

---
#### An example of IPP in the Gaussian model (Neyman and Scott'48)
Gaussian model with incidental parameter (i.e. FE $(\alpha_i)_i$) and a structural paremeter (unknow variance $\sigma^2$): $i\in[n]$ and $j\in[T]$
$$
X_{ij} = \alpha_i + \sigma g_{ij}, \mbox{ where } g_{ij}\overset{i.i.d.}{\sim} \cN(0,1) $$
- MLE is $\hat \alpha_i = \bar{X}_{i\cdot}, i\in[n]$ and 
$$
\hat \sigma^2 = \frac{1}{nT} \sum_{i=1}^n \sum_{j=1}^T \big(X_{ij} - \bar{X}_{i\cdot}\big)^2 \sim \sigma^2 \frac{\chi^2[n(T-1)]}{nT}.
$$
- $\hat\sigma^2$ is <span style="color: blue;"> not consistent</span>  as $n\to\infty$ (and fixed $T$): indeed, for all $n,T$,
$$
\bE[\hat\sigma^2] = \sigma^2 \frac{T-1}{T} \mbox{ and } \bV[\hat\sigma^2] = 2 \frac{(T-1)}{n T^2}.
$$
(*Note:* A consistent estimator with a bounded variance is asymptoticall unbiased)
<!-- --- 

 #### The IPP in network formation (G '17, J '18) 

![100%](ipp_graham.png) -->

---

#### The IPP in the Poisson model for bi-partite graphs (FW '18)

![100%](ipp_2w.png)



---
### A key idea: the diff-in-diff (DiD) - example in linear regression

**Problem:** how to get rid of the fixed effects so that we can just estimate $\beta$?

**The DiD in the linear regression model with fixed effects**
$$ Z_{ij} = \alpha_i + \delta_j + <X_{ij}, \beta> + \epsilon_{ij}.$$
We observe that
$$Z_\xi = (Z_{ij} - Z_{i j^\prime }) - (Z_{i^\prime j} - Z_{i^\prime j^\prime}) = < \tilde{X}_{\xi}, \beta>  + \epsilon_{\xi}$$
where
$$\xi = \begin{pmatrix} i & j \\ i^\prime & j^\prime \end{pmatrix} \mbox{ and } \tilde{X}_\xi =  (X_{ij} - X_{i j^\prime }) - (X_{i^\prime j} - X_{i^\prime j^\prime})$$

This can be done for any <span style="color: blue;"> tetrads </span>  $\xi$. 



---
###  The DiD strategy in Poisson regression: sufficient statistics for the FE

<div class="block">
  <div class="block-content">
    <div align="center">
 How can we proceed the diff-in-diff trick in our Poisson regression model? 
 
 Go for <span style="color: blue;"> CMLE (conditional MLE)</span>. 
    </div>
  </div>
</div>

The log-likelihood function is (up to a constant independent of the parameters)
$$
\begin{align}
&(\beta, (\alpha_i), (\delta_j))  \to \sum_{i} d_{i\cdot} \alpha_i + \sum_{j} d_{\cdot j} \delta_j + \sum_{ij} Y_{ij} <X_{ij}, \beta> - \exp(\alpha_i + \delta_j + <X_{ij}, \beta>)
\end{align}
$$
where

$$
d_{i \cdot} = \sum_{j} Y_{ij} \mbox{ is the degree of } i \mbox{ and } d_{\cdot j} = \sum_{i} Y_{ij} \mbox{ is the degree of } j.
$$
Hence, **the degrees are sufficient statistics for the FE**


---
### Recap on sufficient statistics

> #### Definition
> If the likelihood function can be written as
> $$\ell(\theta) = \exp\big( h(Y). g(\theta, S(Y))\big)$$
> then $S(Y)$ is a <ins>sufficient statistics</ins> for parameter $\theta$.

> #### Definition
> If the likelihood function  for $\theta=(\beta, \gamma)$ can be written as
> $$\ell(\theta) = \exp\big( h(Y, \beta) . g(S(Y), \beta, \gamma)\big)$$
> then $S(Y)$ is a <ins>sufficient statistics</ins> for parameter $\gamma$.


---
### CMLE = conditional Maximum likelihood Estimation

> #### Idea
> Conditionning on a sufficient statistics for $\gamma$ (a nuisance parameter) removes $\gamma$ from the likelihood function.

$$
\begin{align}
&\mathbb{P}_{\theta}[Y=y| S(Y) = S(y)] = \frac{\mathbb{P}_\theta[Y=y \mbox{ and } S(Y) = S(y)]}{\mathbb{P}_\theta[S(Y) = S(y)]} = \frac{\mathbb{P}_\theta[Y=y]}{\mathbb{P}_\theta[S(Y) = S(y)]} \\
& = \frac{e^{h(y, \beta)} \color{red}{e^{g(S(y),\theta)}}}{ \sum_{z: S(z)=S(y)} e^{h(z, \beta)} \color{red}{e^{g(S(z),\theta)}}} = \frac{e^{h(y, \beta)}}{ \sum_{z: S(z)=S(y)} e^{h(z, \beta)}}: = \ell(\beta, y)
\end{align}
$$

The idea of CMLE is to maximize $\beta\to \log \ell(\beta, Y)$ (where $Y$ is my data).


---
### Why CMLE works?

> #### Theorem (CMLE principle)
> Let $S(Y)$ be a sufficient statistics for $\gamma$. Denote 
>$$
\mathcal{L}(\beta, y):= \log \mathbb{P}_{(\beta, \gamma)}[Y=y| S(Y) = S(y)] \mbox{ (which is independent of }\gamma)$$ 
> Let $\beta^*$ and assume that $Y\sim \mathbb{P}_{\theta^*}$ for $\theta^*=(\beta^*, \gamma^*)$ - whatever $\gamma^*$ is. 
>Then 
>$$
\beta\to \mathbb{E}_{\theta^*} \mathcal{L}(\beta, Y)$$
>is maximal at $\beta = \beta^*$.

---
### Proof of the CMLE principle
Assume that the pdf of $Y$ is of the shape $p_\theta(y)=g(y, \beta)h(S(y), \theta)$ under $\mathbb{P}_\theta$.
<u>Step 1:</u> Law of iterated expectation:
$$
\mathbb{E}_{\theta^*} \mathcal{L}(\beta, Y) = \mathbb{E}_{\theta^*}\left[ \mathbb{E}_{\theta^*}\left[\mathcal{L}(\beta, Y)| S(Y)\right]\right]. $$

<u>Step 2:</u> For all $s$, we have 
$$
\mathbb{E}_{\theta^*}\left[\mathcal{L}(\beta, Y)| S(Y)=s\right] = \mathbb{E}_{\beta^*}\left[ \log f_{\beta}(Z) \right].
$$

where $f_{\beta}(z)= \frac{g(z,\beta)}{\sum_{z:S(z)=s} g(z, \beta)}$ is the pdf of $Z=(Y|S(Y)=s)$ under $\mathbb{P}_{\theta}$

<u>Step 3:</u> From Jensen's inequality, we get
$$
\mathbb{E}_{\beta^*}\left[ \log f_{\beta}(Z) \right]\leq \mathbb{E}_{\beta^*}\left[ \log f_{\beta^*}(Z) \right].\hspace{1cm} \square
$$

---
### CMLE in our Poisson model
Let $
S(y) = \left(\left(\sum_j y_{ij}\right)_i, \left(\sum_i y_{ij}\right)_j\right)$ be the vector of all degrees of graph $y$: we know that $S(Y)$ is a sufficient statistics for all FEs. Let $\theta=(\beta, (\alpha_i), (\delta_j))$

$$
\begin{align}
&\mathbb{P}_{\theta}[Y=y| S(Y) = S(y)] = \frac{\mathbb{P}_\theta[Y=y]}{\mathbb{P}_\theta[S(Y) = S(y)]} = \frac{\prod_{ij} \frac{\lambda_{ij}^{y_{ij}}}{y_{ij}!}e^{-\lambda_{ij}}}{\sum_{z: S(z)=S(y)} \prod_{ij} \frac{\lambda_{ij}^{z_{ij}}}{z_{ij}!}e^{-\lambda_{ij}}}\\
& = \left(\sum_{z: S(z)=S(y)} \bigg(\prod_{ij} \lambda_{ij}^{z_{ij}-y_{ij}}\bigg) \bigg(\prod_{ij} \frac{y_{ij}!}{z_{ij}!}\bigg)\right)^{-1}
\end{align}
$$

and for all $z$ and $y$ having the same degrees (i.e. $S(y)=S(z)$):

$$
\bigg(\prod_{ij} \lambda_{ij}^{z_{ij}-y_{ij}}\bigg) =  \exp\bigg(\sum_{ij}(\alpha_i + \delta_j + <X_{ij}, \beta>)({z_{ij}-y_{ij}})\bigg) = \exp\bigg(<\sum_{ij}({z_{ij}-y_{ij}}) X_{ij}, \beta>\bigg)
$$

---
### CMLE in our Poisson model
**All FEs diseappered from the conditional likelihood function:**

$$
\log \mathbb{P}_{\theta}[Y=y| S(Y) = S(y)] = -\log\left(\sum_{z: S(z)=S(y)} \exp\bigg(<\sum_{ij}({z_{ij}-y_{ij}}) X_{ij}, \beta>\bigg)  \bigg(\prod_{ij} \frac{y_{ij}!}{z_{ij}!}\bigg)\right) 
$$

hence, the conditional maximum likelihood estimator is $\hat \beta$ minimizing

$$
\beta \to \log\left(\sum_{z: S(z)=S({\color{red}{Y}})} \exp\bigg(<\sum_{ij}({z_{ij}-{\color{red}{Y}_{ij}}}) X_{ij}, \beta>\bigg)  \bigg(\prod_{ij} \frac{{\color{red}{Y}_{ij}}!}{z_{ij}!}\bigg)\right) 
$$

--- 
### But the sum $\sum_{z: S(z)=S(Y)}$ is not computationally feasible!

> #### Problem
> It is not possible to construct the conditional log-likelihood function  
> $$
\beta \to \log\left(\sum_{{\color{red}{z: S(z)=S(Y)}}} \exp\bigg(<\sum_{ij}({z_{ij}-Y_{ij}}) X_{ij}, \beta>\bigg)  \bigg(\prod_{ij} \frac{Y_{ij}!}{z_{ij}!}\bigg)\right) 
$$



However, we don't have to take all $z$ such that $S(z)=S(Y)$, we may restrict ourself to a subset of them: look at <u>tetrads</u> and use a <u>Diff-in-Diff argument</u> on $\log(\lambda_{ij})$!


---
###  The diff-in-diff strategy in our Poisson regression model

Let $\xi = \begin{pmatrix} i & j \\ i^\prime & j^\prime \end{pmatrix}$ be a tetrad. We have


$$ \underbrace{ \big(\ln\lambda_{ij} - \ln\lambda_{ij^\prime}\big) - \big(\ln\lambda_{i^\prime j} - \ln\lambda_{i^\prime j^\prime}\big)}_{\text{cancel } \alpha_i, \alpha_{i^\prime}, \delta_j, \delta_{j^\prime}} = <\beta, \tilde X_\xi> $$

where $\tilde X_\xi$ is the tetrad feature: $\tilde{X}_\xi =  (X_{ij} - X_{i j^\prime }) - (X_{i^\prime j} - X_{i^\prime j^\prime})$

>We define the <u>DiD sign matrix $s_\xi$ w.r.t. tetrad $\xi$</u> at edge $(i_0,j_0)$ by 
>$$
s_\xi(i_0j_0) = 
\begin{cases}
0  \mbox{ if } (i_0,j_0) \mbox{ is not an edge of } \xi\\
(\mathbf{1}(i_0 = i) - \mathbf{1}(i_0 = i^\prime))(\mathbf{1}(j_0 = j) - \mathbf{1}(j_0 = j^\prime)) & \mbox{ otherwise.}
\end{cases}
$$

$$
\sum_{\mbox{edge in } \xi} s_\xi(edge) \ln \lambda_{edge} = \big(\ln\lambda_{ij} - \ln\lambda_{ij^\prime}\big) - \big(\ln\lambda_{i^\prime j} - \ln\lambda_{i^\prime j^\prime}\big) = <\beta, \tilde X_\xi>
$$

---

### The DiD in (conditional) likelihood for a given tetrad

- <u>*Question:*</u> Given a graph $y$, how to construct a new graph $z$ such that
$$ \ln \mathbb{P}_{\theta}\left( Y = z \right) - \ln \mathbb{P}_{\theta}\left( Y = y \right) = \sum_{i,j} {\color{red} (z_{ij} -  y_{ij})} \ln \lambda_{ij}(\theta) - (\ln z_{ij}! - \ln y_{ij}!)$$
where $\theta=(\beta, (\alpha_i)_i, (\delta_j)_j)$ and $\ln\lambda_{ij}(\theta) = \alpha_i + \psi_j + <X_{ij}, \beta>$, is <u>**not**</u> a function of the fixed effects $(\alpha_i)_i, (\delta_j)_j$?

- <u>*Answer:*</u> Take a polyad $\xi$ and let $z_{ij} - y_{ij}$ be a multiple of the DiD sign  $s_\xi(ij)$:
<br>

$$
z:= T_\xi^r(y) := y + r s_\xi, \mbox{ i.e. } z_{ij} = y_{ij} + r s_\xi(ij), \mbox{ for } r\in \mathbb{Z}
$$

---

### The set of valid $r$'s defines an orbit of graphs $\cO_\xi(y)$ for $\xi = \begin{pmatrix} i_1 & i_2\\ i_1^\prime & i_2^\prime \end{pmatrix}$

![100%](orbits.png)

---

### A multiclass classification problem for each tetrad $\xi$

![100%](orbits_details.png)

---
### A multiclass classification problem for each tetrad $\xi$

> #### Definition
> For every tetrad $\xi$ we let the orbit of $y$ be:  
> $$
\cO_\xi(y) := \left\{ T_\xi^r(y): -m_\xi(y) \leq r \leq M_\xi(y) \right\} $$
> where 
>$$m_\xi(y) = \min(y_{ij}:s_\xi(ij)=1) \mbox{ and } M_\xi(y)= \min(y_{ij}: s_\xi(ij)=-1).$$


- <u>To design a loss function:</u> for each $\xi$, we look at our data as a multiclass classification problem. The number of classes is $1+m_\xi(y)+M_\xi(y)$

- A multiple multi-class classification problems dataset $(\tilde{X}_\xi, Y_\xi=0)_\xi$ where $Y_\xi=0$ is the class $0$ observed among all classes $\{-m_\xi(Y) \leq r \leq M_\xi(Y)\}$



---

### Designing a loss function from the tetrads' classification problems

- The set of <u>*active tetrads*</u> is 

$$
\Xi_a := \left\{\xi: m_\xi(y)+M_\xi(y) \geq1 \right\}
$$
(If $m_\xi(y)+M_\xi(y)=0$, there is no classification problem)

<!-- - Permuting $i_d \leftrightarrow i'_d$ in $\xi$ flips the signs, but yields the same problem. -->

</br>

>#### Loss function and the tetrads estimator
> Our loss function is $\beta\to \widehat{L}(\beta) = \sum_{{\color{red}\xi \in \Xi_a}} \ell_\xi(\beta | Y)$ where for all $\xi$ and $y$
>$$ \ell_\xi(\beta | y) = -\ln \mathbb{P}_\beta( Y = y | {\color{red}{Y \in \mathcal{O}_\xi(y)}} ). $$
> The **tetrads estimator** is $\widehat{\beta}_{\Xi_a} = \arg\min_\beta \widehat{L}(\beta)$.



---
### Computational properties of the loss function
> Newton's method to construct the tetrads estimator $\widehat{\beta}_{\Xi_a}$: $
{\color{red}{\beta_{k+1} = \beta_{k} - \widehat{H}_k^{-1}\widehat{S}_k}} 
$
where $\widehat{H}_k = \nabla^2 \widehat{L}(\beta_k)$ and $\widehat{S}_k = \nabla \widehat{L}(\beta_k)$.

We have for all tetrads $\xi$ and graph $y$:
$$ 
\begin{align*}
&\ell_\xi(\beta | y) = \ln \left(\sum_{r=-m_\xi(y)}^{M_\xi(y)} \exp\left( r <\tilde{X}_\xi, \beta> + \sum_{ij}\ln \frac{y_{ij}!}{(y_{ij} + r s_{\xi}(ij))!}\right) \right) \\
&\nabla \ell_\xi(\beta | y) = \left( \bE_\beta[m_\xi(Y)|Y \in\cO_\xi(y)]-m_\xi(y) \right)\widetilde{X}_\xi \\ 
&\nabla^2 \ell_\xi(\beta | y) = \left( \bV_\beta[m_\xi(Y)|Y \in\cO_\xi(y)]\right)\widetilde{X}_\xi \widetilde{X}_\xi^\top
\end{align*}
$$

- It is strictly convex as long as $\widetilde{X}_\xi \widetilde{X}_\xi^T \succ 0$.
- Computational tricks to sum over all active tetrads.

---

### Try it on Colab

We use [Lucas Resende's package](https://github.com/lucasresenderc/polyads):

- first on synthetic data for a two-way model:
$$
\lambda_{ij} = \exp(\alpha_i + \delta_j + \beta_0 X_{ij}^{(0)} + \beta_1 X_{ij}^{(1)})
$$
- then on the trade data from Santos Silva & Tenreyro (2006) -- for only $20$ countries
- then we will go to synthetic data from a three-ways model.



<div align="center">
  <div style="border: 2px solid #34495e; border-radius: 8px; padding: 15px 30px; display: inline-block; background-color: #ecf0f1; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">

**[link to Colab](https://colab.research.google.com/drive/1Q3Ycqqb5lazOo2Agn2c4t731OK3clcGh?usp=sharing)**

  </div>
</div>

---

### Extension to <u>multi-ways models</u>: A 'trade data' example

- **Trade data**: in the literature on gravity models for trade there is interest in learning from 4-dimensional data where
    - $i_1$ is an exporter country;
    - $i_2$ is an importer country;
    - $i_3$ is the industry;
    - $i_4$ is the time.
- Measuring $Y_{i_1 i_2 i_3 i_3}$ as the volume of trade and taking $X_{i_1 i_2 i_3 i_4}$ as the presence (or amount) of tariffs from $i_1$ to $i_2$ in industry $i_3$ at time $i_4$ we can measure the impact of tariffs.

---
### Extension to the <u>multi-ways model</u>

- $i_1 \in [n_1]$, $i_2 \in [n_2]$, ..., $i_D \in [n_D]$, $n = \prod_{d=1}^D n_d$
- $Y_{i_1i_2\dots i_D} \geq 0$ and $X_{i_1i_2\dots i_D} \in \mathbb{R}^p$
- $\mathbf{i} = (i_1,i_2,\dots, i_d) \in \prod_{d=1}^D [n_d]$
$$\mathbb{P}_{\beta_\star, \theta_\star}\left( Y = y | X \right) = \prod_{\mathbf{i}} e^{-\lambda_{\mathbf{i}}(\beta_\star,\theta_\star)}\frac{\lambda_{\mathbf{i}}(\beta_\star,\theta_\star)^{y_\mathbf{i}}}{y_\mathbf{i}!} $$
- $\lambda_{\mathbf{i}}(\beta,\theta) = \exp\left\{ \beta^TX_{\mathbf{i}} + \theta^{(1)}_{i_2i_3\dots i_D} + \theta^{(2)}_{i_1i_3\dots i_D} + \cdots + \theta^{(D)}_{i_1i_2\dots i_{D-1}} \right\}$
-  $\beta\in\mathbb{R}^p$ is the parameter of interest. $\theta$ is a vector containing the fixed effects (incidental parameters).

---

###  The IPP in Poisson ML for 3-way model (WZ '21)

![100%](ipp_3w.png)

---

### Introducing polyads in multi-ways models

- A <u>*polyad*</u> is a pair of edges $\mathbf{i}=(i_d), \mathbf{i}'=(i_d')$ such that $i_d \neq i_d'$ for all $d\in[D]$:
$$\xi = \begin{bmatrix}i_1 & i_2 & \cdots & i_D\\ i_1' & i_2' & \cdots & i_D'\end{bmatrix}$$
Note: we can form $2^D$ edges in a polyads.
- The <u>*diff-in-diff sign tensor $s_\xi$*</u> is defined for all edge $\mathbf{j} = (j_d)_d$ as 
$$
s_\xi(\mathbf{j}) = \prod_{d=1}^D \big(\mathbf{1}(i_d = j_d) - \mathbf{1}(i_d^\prime = j_d^\prime)\big)
$$

---
###  The diff-in-diff strategy in the conditional likelihood for each polyad

- diff-in-diff works in the multi-way case:
$$ \underbrace{\sum_{ \mathbf{j} \in \prod_{d=1}^D \{i_d, i_d'\}}  s_\xi(\mathbf{j}) \ln\lambda_\mathbf{j}}_{\text{diff-in-diff of }\ln\lambda} = <\beta^T, \widetilde{X}_\xi> \mbox{ where } \widetilde{X}_\xi:=  \underbrace{\sum_{\mathbf{j} \in \prod_{d=1}^D \{i_d, i_d'\}} s_\xi(\mathbf{j})  X_{\mathbf{j}} }_{\text{diff-in-diff of X}}  $$

 >#### Loss function and the polyads estimator (same definition as $D=2$)
> Our loss function is $\beta\to \widehat{L}(\beta) = \sum_{{\color{red}\xi \in \Xi_a}} \ell_\xi(\beta | Y)$ where for all $\xi$ and $y$
>$$ \ell_\xi(\beta | y) = -\ln \mathbb{P}_\beta( Y = y | {\color{red}{Y \in \mathcal{O}_\xi(y)}} ), $$
> $
\cO_\xi(y) := \left\{y + r s_\xi: -m_\xi(y) \leq r \leq M_\xi(y) \right\} 
$, $m_\xi(y) = \min(y_{\mathbf{i}}:s_\xi(\mathbf{i})=1)$,  $M_\xi(y)= \min(y_{\mathbf{i}}: s_\xi(\mathbf{i})=-1)$ and the **polyads estimator** is $\widehat{\beta}_{\Xi_a} = \arg\min_\beta \widehat{L}(\beta)$.




---

### Definitions of Density and sparsity of a graph

- The <u>*density of a graph*</u> is given by
$$ \rho = \frac{|E|}{n} \mbox{ where } E = \{ \mathbf{i} : y_\mathbf{i} > 0 \}. $$

- We say that a sequence of graphs $(y_{(k)})_{k>0}$ is <u>*sparse*</u> if $\rho_{(k)} \to 0$ and $n_{(k)} \to \infty$ as $k\to\infty$.

<br>

**Ex.:** Social networks typically have $\rho_{(k)} = O\left(\frac{1}{\sqrt{ n_{(k)}}}\right)$.

---

##### Statistical properties
# Consistency

Let $M_\lambda = \max_{\mathbf{i}} |\ln\lambda_{\mathbf{i}}|$. If $Y$ follows the Poisson multi-way model and some technical conditions hold (boundness of the risk and separability of the minimum), then:
- Conditionaly on $X$, $\widehat{\beta}_{\Xi_a} \to \beta_\star$ in probability as $\rho \gg \frac{M_\lambda}{n}$.

---

##### Statistical properties
# Asymptotic normality

- Adding other technical conditions, it holds $\forall v \in \mathbb{R}^p$, $\|v\|=1$, that
$$ \frac{ \langle \widehat{\beta}_{\Xi_a} - \beta_\star , v \rangle }{ \sqrt{ v^ T (\nabla^2\widehat{L}_{\Xi_a}^{-1}) \widehat{\Sigma}_{\Xi_a} (\nabla^2\widehat{L}_{\Xi_a}^{-1}) v } } \to \mathcal{N}({\color{red} 0},1) \text{ as } \rho \gg \frac{M_\lambda}{n}$$
where $\widehat{\Sigma}_{\Xi_a} = \sum_{\xi, \xi' \in \Xi_a} \left(\nabla \ell_\xi \right)\left(\nabla \ell_\xi \right)^T \mathbf{1}_{\xi \text{ and }\xi'\text{ share at least one edge}}$.

- In the worst case, $\widehat{\Sigma}_{\Xi_a}$ can be evaluated in $O(|E|^3)$. Typically it requires $O(|E|^2)$. 

---

### Looping over <u>active</u> polyads in Newton's method
## The total number of polyads

![100%](combinations_polyads.png)

---

### Looping over <u>active</u> polyads in Newton's method
## A computational trick

![100%](all_lines.png)
- If a $\xi$ is active, then $\min_{\mathbf{i}: s_\xi(\mathbf{i})}y_{\mathbf{i}} > 0$, thus $y_\mathbf{i} > 0$, $y_\mathbf{i'} > 0$ (up to permutation).

---
### Looping over <u>active</u> polyads in Newton's method
## A computational trick

- Instead of looking at all $O(n^2)$ possible polyads we can search over all pairs $(\mathbf{i}, \mathbf{i'})$ such that $y_\mathbf{i} > 0$ and $y_\mathbf{i'} > 0$.


- This can be done in $O(|E|^2)$ where $E = \{ \mathbf{i} : y_\mathbf{i} > 0 \}$.

- It is better than $O(n^2)$ and can even be better than $O(n)$ (PPML).

---

<!-- ##### The many flavours of sparsity
# Density

![100%](def_rho.png)

---

##### The many flavours of sparsity
# Global clustering coefficient

![100%](def_alpha.png)

--- -->

##### Computational experiments
# Data generating setup (from WZ '21)

- 3-way DGP: $n_1=n_2$ vary and $n_3=5$ is fixed.
- $\theta_{ij}, \theta_{it}, \theta_{jt}$ are i.i.d. normal with zero mean and variance $1/16$. $\beta_\star = 1$.
- The features are correlated with $\theta$ and with previous features in the 3rd axis:
$$X_{ijt} = \begin{cases} \frac{1}{2}X_{ij(t-1)} + \theta_{it} + \theta_{jt} + \frac{1}{4}\mathcal{N}(0,1) \text{, if }t>1\\ \theta_{it} + \theta_{jt} + \frac{1}{4}\mathcal{N}(0,1) \text{, if }t=1 \end{cases}$$
- We let $\mathbb{E}(Y_{ijt}) = \exp\left( c + \beta_\star X_{ijt} + \theta_{ij} + \theta_{it} + \theta_{jt} \right).$
- The constant $c$ let us control the density. We consider $Y_{ijt}$ Poisson and NB.

---

##### Computational experiments
# The initial example
<!-- _class: example -->

![100%](distributions_setup_1s.png)
- Coverage of the 95% C.I. ($n_1=100$): 81%(PPML), 97%(PPML debiased), 94% (Polyads). **We have a good concentration even when $n_1=50$.**

---

##### Computational experiments
# Short panel ($n_1=n_2=50$, $n_3=5$)
<!-- _class: example -->

![100%](setup_1_False_50.png)

---

##### Computational experiments
# Short panel ($n_1=n_2=100$, $n_3=5$)
<!-- _class: example -->

![100%](setup_1_False_100.png)

---

##### Computational experiments
# Short panel ($n_1=n_2=50$, $n_3=5$, NB)
<!-- _class: example -->

![100%](setup_1_True_50.png)

---

##### Computational experiments
# Short panel ($n_1=n_2=100$, $n_3=5$, NB)
<!-- _class: example -->

![100%](setup_1_True_100.png)

---

##### Computational experiments
# Sparse case ($\rho = \frac{4}{\sqrt{n}}$, NB)
<!-- _class: example -->

![100%](setup_1_True_sparse.png)

---
### Causal inference via structural parameter estimation on panel data

<u> Context:</u> We study health insurance claims data over the years 2016 to 2018.

In May 2017, the fees charged by general practitioners (GPs) belonging to the regulated sector (sector~1) have increased by 8.7\%.

We find that the stronger financial incentives have caused physician activity (as measured by number of visits) to rise by approximately 10\%

<u>Questions about accessibility:</u> Did this policy induce any change in gender homophily between patients and general practitioners (GPs)?

Did patient prefer more medical offices that are located in the same municipality?

 
<u> Solution</u> Using a  three-way model and controlling for dyads fixed effects allows to estimate how the reform has changed the doctor-patient connections.

---
### Causal inference via structural parameter estimation on panel data

<u> Data aggregation:</u> We aggregate data at the city-sex level:  index $i$ (resp. $j$) stands thus for the set of patients (resp. doctors) in a given municipality with given gender.

<u>Outcome:</u> $Y_{ijt}$ is the number of visits by patient $i$ to doctor $j$ on month $t$. 

<u>Features construction (1/2):</u>
The treatment $T_{j}$ is a binary variable equal to 1 for sector 1 GPs, and to 0 for direct access specialists. 

The reform has been implemented from May 2017 onward, hence the definition of $\text{Post}_t$, a dummy variable equal to 1 after that date. 



---
### Causal inference via structural parameter estimation on panel data

<u>Features construction (2/2):</u>
- the interactions between $\text{Post}_t \times T_j$ 
- a dummy variable equals to 1 when patients and doctors have the same sex,  
- a dummy variable that is equal to 1 when the medical office chosen is located in the same municipality as the patient's home,  
- travel time (measured in minutes between the centroids of municipalities).

<u>Model:</u> A three-way Poisson model $Y_{ijt}\sim\mathcal{P}(\lambda_{ijt})$ with intensity given by

$$
\ln\lambda_{ijt}=\big(\beta_\texttt{d}  d_{ij}+\beta_\texttt{sc} \mathbf{1}\{\text{city}_i=\text{city}_j\}+\beta_\texttt{ss} \mathbf{1}\{\text{sex}_i=\text{sex}_j\}\big) \times \text{Post}_t \times T_j  +u_{ij}+v_{jt}+w_{it}.
$$

---
### Causal inference via structural parameter estimation on panel data

$$
\ln\lambda_{ijt}=\big(\beta_\texttt{d}  d_{ij}+\beta_\texttt{sc} \mathbf{1}\{\text{city}_i=\text{city}_j\}+\beta_\texttt{ss} \mathbf{1}\{\text{sex}_i=\text{sex}_j\}\big) \times \text{Post}_t \times T_j  +u_{ij}+v_{jt}+w_{it}.
$$

<u>Parameter interpretation:</u> 
- $\beta_\texttt{d}$: additional effect of the distance after the reform
- $\beta_\texttt{sc}$: additional effect of living in the same city after the reform 
- $\beta_\texttt{ss}$: additional effect of homophily gender after the reform

---
### Causal inference via structural parameter estimation on panel data


<style scoped>
table {
    width: auto;
    height: auto; /* This stops the table from pushing text off the screen! */
    margin: 0 auto;
}
</style>

<u>Result on SNDS:</u> 95% confidence intervals (in parentheses) by subsample proportion and method (100 replications). $\beta_\texttt{d}$ estimates are scaled by $10^4$; $\beta_\texttt{sc}$ and $\beta_\texttt{ss}$ by $10^2$.


| Parameter | 2% Subsample | 3% Subsample | 4% Subsample |
| :--- | :---: | :---: | :---: |
| $\beta_\texttt{d} (\times 10^{4})$ | 1.23 <small>(0.26, 2.20)</small> | 1.73 <small>(1.18, 2.28)</small> | 1.45 <small>(1.03, 1.86)</small> |
| $\beta_\texttt{sc} (\times 10^{2})$ | -7.60 <small>(-13.10, -2.10)</small> | -3.91 <small>(-6.55, -1.27)</small> | -4.52 <small>(-6.28, -2.75)</small> |
| $\beta_\texttt{ss} (\times 10^{2})$ | -2.48 <small>(-4.45, -0.50)</small> | -0.35 <small>(-1.61, 0.92)</small> | -0.20 <small>(-1.13, 0.73)</small> |

<br>

<u>Interpretation:</u>
- a negative coefficient means that after the reform patients are more likely to visit a doctor outside their own city
- Having $0$ in the confidence interval means we cannot tell about the effect of the reform

---

##### Conclusion
# Our contributions

- Multi-way.
- Faster than PPML on sparse networks.
- No IPP problem by construction.
- Convex loss with good convergence.
- Reliable confidence intervals under model assumptions.

<!-- ---

##### Conclusion
# What is next?

- Investigate the IPP problem in higher dimensions: can the PPML have a IPP in consistency in 4-way or 5-way setups?
- Investigate the IPP under sparsity: does it gets worse?
- Robustness to $EY = \lambda$.
- Better exploit the structure of the fixed effects.
- Our algorithm can be used to generalize and improve the computational time of other similar methods.
- Release a Python package. -->

