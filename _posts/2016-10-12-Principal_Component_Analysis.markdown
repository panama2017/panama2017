---
layout:     post
title:      "Principal Component Analysis 0"
subtitle:   "Derivation"
date:       2016-10-12
author:     "Baoxiang Pan"
header-img: "img/home.jpg"
series: "Principal Component Analysis"
comments: true
---

[$$PCA$$\|Principal Component Analysis](https://en.wikipedia.org/wiki/Principal_component_analysis) is a popular and effective feature extraction method. It has been widely used in meteorology since Edward N. Lorenz introduced it in the 1956 [paper](http://www.o3d.org/abracco/Atlantic/Lorenz1956.pdf). The idea behind it is elegant. But I always fail to recall its proof every time I wanted to use it. Now I decided to mark it down here as a forever reminder. This post consists of the theoretical part while there would be a case study to illustrate the ideas later.



For a multi-dimensional random variable sample set with dimension of $$m$$ and sample size of $$n$$, we denote it as $$D$$, here $$D$$ is a $$m \times n$$ matrix, each row corresponds to the realization series of one dimensional random variable and each colum corresponds to one realization of the multi-dimensional random variable vector. 

It is pre-assumed that there is information redundance in the original $$m$$ dimensional representation of the random variable vector. In other words, variables in different dimensions are somehow dependent. $$PCA$$ is used to detect and eliminate the linear correlation between dimensions. After $$PCA$$ processing, we reach an uncorrelated and simplified representation of the initial random variable vector(There is another method named Independent Component Analysis which applies a linear transform to remove the dependence of Gaussian Random Variables, which I may talk about in later posts).  

I mentioned "information" in the above paragraph without a strict definition of it. In the context of probability theory, information is a characteristic captured by a functional of probability distribution  function named entropy:


\\[E(x)=-\int p(x)logp(x)dx \\]

The information redundance is:

$$
\sum_{i=1}^{m}E(X_i)-E(X_1,X_2,...X_m)
$$

We can see that if $$X_i(i=1,2,...m)$$ are independent random variables, the information redundance is $$0$$. Here in the context of decorrelation operation, the covariance/correlation matrix is applied to denote information redundance. Specifically, the magnitude of the non-diagonal elements in the covariance/correlation matrix denote how correlated or how much redundant information there is. If $$X_i(i=1,2,...m)$$ are uncorrelated random variables, the non-diagonal elements are 0 and there is no information redundance in a 2nd order central moment manner(Yes there is possible redundance in other moments).

Either to use covariance matrix or correlation matrix in $$PCA$$ depends on the purpose of the transformation, as will be explained later. Covariance matrix($$Cov$$) and correlation matrix($$Corr$$) for a $$m$$ dimensional random vector are estimated as follows:


$$
Cov=
        \begin{pmatrix}
        x^c_{11} & x^c_{12} &...& x^c_{1n} \\
        x^c_{21} & x^c_{22} &...& x^c_{2n} \\
        ...\\
        x^c_{m1} & x^c_{m2} &...& x^c_{mn} \\
	\end{pmatrix}
	
        \begin{pmatrix}
        x^c_{11} & x^c_{12} &...& x^c_{1n} \\
        x^c_{21} & x^c_{22} &...& x^c_{2n} \\
        ...\\
        x^c_{m1} & x^c_{m2} &...& x^c_{mn} \\
	\end{pmatrix}^{T}=X_cX_c^{T}
$$
   


$$
Corr=
        \begin{pmatrix}
        x^n_{11} & x^n_{12} &...& x^n_{1n} \\
        x^n_{21} & x^n_{22} &...& x^n_{2n} \\
        ...\\
        x^n_{m1} & x^n_{m2} &...& x^n_{mn} \\
	\end{pmatrix}
	
        \begin{pmatrix}
        x^n_{11} & x^n_{12} &...& x^n_{1n} \\
        x^n_{21} & x^n_{22} &...& x^n_{2n} \\
        ...\\
        x^n_{m1} & x^n_{m2} &...& x^n_{mn} \\
	\end{pmatrix}^{T}=X_nX_n^{T}
$$

Here $$x^c_{ij}=x_{ij}-\bar{x_{i}}$$ and $$x^n_{ij}=\frac{x_{ij}-\bar{x_{i}}}{\sigma_{x_i}}$$.

We desire an invertable transform applied on $$X_c$$ or $$X_n$$ to make $$Cov$$ or $$Corr$$ diagonal. Take $$Cov$$ as example, the most intuitive form is a linear transformation $$A$$:

$$
(AX_c)(AX_c)^T=Cov_{D}
$$

which can be reorganized as:


$$
(X_cX_c^T)A^T=A^{-1}Cov_{D}
$$

All the magic lies in the design of $$A$$. Beautiful theories are hard to find but once they are found it's much easier to prove and trace back. Let me be direct here. If each row of $$A$$ is composed of the eigen vector of $$X_cX_c^T$$ and they are orthogonal with each other, then $$Cov_{D}$$ is diagonal. Thus, if the original random vector is represented in the vector space whose basis are the orthogonal eigen vectors of the original covariance matrix, the 2nd order information redundance would be eliminated. This is the core idea of $$PCA$$.









For a better comprehension, the deduction process here will be presented in a backtracking manner. The linear correlation between dimensions can be represented by the correlation matrix (denote as $$corr$$ afterwards):

$$
corr=
        \begin{pmatrix}
        \rho_{11} & \rho_{12} &...& \rho_{1m} \\
        \rho_{21} & \rho_{22} &...& \rho_{2m} \\
        ...\\
        \rho_{m1} & \rho_{m2} &...& \rho_{mm} \\
	\end{pmatrix}
$$
   
Here $$\rho_{ij}$$ is the correlation coefficient between the $$i$$th dimension $$x_i$$ and $$j$$th dimension $$x_j$$:

$$
\begin{align*}
\rho_{ij}&=E[\frac{x_i-\mu_i}{\sigma_i}\frac{x_j-\mu_j}{\sigma_j}] \\
	 &\approx\frac{1}{n}\sum_{k=1}^{n} (\frac{x_{ik}-\mu_i}{\sigma_i}\frac{x_{jk}-\mu_j}{\sigma_j}) \\
\end{align*}
$$

$$\mu$$ represents mean and $$\sigma$$ represents standard variance.

The more elegant  matrix representation of $$corr$$ is as follows:

\\[corr=D_ND_N^{T}\\]

$$D_N$$ is normalized $$D$$, specifically, each element $$x_{ij}^{N}$$ in $$D_N$$ equals to its correspondent element $$x_{ij}$$
 in $$D$$ minus the mean value $$\mu_i$$ then divided by the standard variance $$\sigma_i$$:

\\[x_{ij}^{N}=\frac{x_{ij}-\mu_{i}}{\sigma_i} \\]



$$corr$$ is a symmetric matrix according to its definition.
Its diagonal elements all equal to $$1$$ according to the definition of variance, while the non-diagonal elements are within $$[0,1]$$ according to Cauchy–Schwarz inequality. The larger the non-diagonal element is, the more redundance we suffer when representing the corresponding two variables seperately.

The core of $$PCA$$ is to seek for a better representation of the original data. The new representation is better because there is least correlation between different dimensions as shown in the new $$corr$$. The extreme condition is that the new $$corr$$ is diagonal matrix. We will see that in most real-world cases this is accessible merely through a linear transform of the original data. This method is what we call $$PCA$$.

Linear transform is equivalent to matrix mulplication. Assume that there were a matrix $$A$$, and the new representation of the multi-dimensional random variable sample set should be $$AD$$. It can be easily proved that if the following formula is diagonal:

$$
(AD)(AD)^{T}=
        \begin{pmatrix}
        \lambda_1 & 0 &...& 0 \\
        0 & \lambda_2 &...& 0 \\
        ...\\
        0 & 0 &...& \lambda_m \\
	\end{pmatrix}
$$

then the correlation matrix of $$AD$$ is also dianogal. 


To seek for a linear transfrom is equivalent to construct a matrix be


make a transformation of the original data representation to minimize the non-diagonal elements of t  
![](/img/1stPC.png)


***Comparison of Using Correlation Matrix and Covariance Matrixr
