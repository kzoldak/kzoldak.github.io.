---
layout: post
title: "Fitting a model to data."
comments: true
---

These are my notes on the following paper: [Data analysis recipes: Fitting a model to data](https://arxiv.org/pdf/1008.4686.pdf).


Linear Model
---
$$ 
y=mx+b 
$$
where $$m$$ is slope and $$b$$ is the intercept of the line. 


## Gaussian Distribution's PDF
For this work we will assume that the data $$(x_i, y_i)$$ were drawn from a normal distribution (or Gaussian) with zero mean and known variance of $$\sigma_{y_i}^2$$ about the model. The normal distribution's probability function (as given by [its Wikipedia Page](https://en.wikipedia.org/wiki/Normal_distribution)) is: 

$$
{\displaystyle f(x\mid \mu ,\sigma ^{2})={\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}}
$$

where $$\mu$$ is the mean, $$\sigma^2$$ is the variance (and thus $$\sigma$$ is the standard deviation). 

This function can also be expressed as:

$$
f(x\mid \mu, \sigma^{2}) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{1}{2} \chi^2}
$$

where $$\chi^2$$

$$
\chi^2 = \sum_{i=1}^{N} \left(\frac{x_i-\mu}{\sigma} \right)^2
$$

is the statistic to be minimized during the fitting process. The quotient, $$\left(\frac{x_i-\mu}{\sigma} \right)$$, measures the deviation of $$x$$ from its expected value ($$\mu$$) in units of $$\sigma$$. Thus, $$\sigma$$ defines a length, and this is why minimizing $$\chi^2$$ of a fit gives a metric distance in data space. 

In linear regression, we replace $$x_i$$ with $$y_i$$ and $$\mu$$ with $$y_{model, i}$$ (or $$m x_i + b$$, since the equation of our model is a line). Our $$\sigma$$ becomes $$\sigma_{y_i}$$, the uncertainty on $$y_i$$. 

The $$y_{model, i}$$ is the y-axis value that is estimated for each $$x_i$$ in our data set, given the best-fit model and its parameters (slope and intercept). If we plot $$x_i$$ verses $$y_{model, i}$$, we get a straight line, as we should. Therefore it makes sence that $$y_{model, i}$$ replaces $$\mu$$, a variable used to define the mean of a distribution. 

Acutally, $$y_{model, i}$$ are the means of each data point's statistical probability distributions. The scatter of the data about the linear model can be thought of as the data points being drawn from their own probability distributions. Each $$ith$$ data point was drawn from its own Gaussian distribution (oriented in the y-direction), and $$y_{model,i}$$ at $$x_i$$ is the mean of the $$ith$$ probability distribution. In the simplest form of linear regression, we only work with vertical (y-direction) offsets of the data from the model, hence why we stress these distributions are oriented along the y-axis. 

<!-- The scatter of the data about the linear model can be thought of as the data points being drawn from their own probability distributions (Gaussian). Each $$ith$$ data point was drawn from its own Gaussian distribution (oriented in the y-direction), and $$y_{model,i}$$ at $$x_i$$ is the mean of that distribution. 

The best-fit model's y-axis values (given by $$y_{model, i}$$) ARE the mean of the distribution that the data points are drawn from; at least the mean of the Gaussian distribution that is oriented along the y-axis of each $$ith$$ data point.  -->

Note that it is not uncommon to see different variable names used to represent slope and intercept. $$a$$ is commonly used for slope. 

We now have:

$$
f(y_i \mid x_i, \sigma_{y_i}, m, b) = \frac{1}{\sqrt{2\pi\sigma_{y_i}^2}} \exp\left(-\frac{\left[y_i - y_{model,i}\right]^2}{2 \sigma_{y_i}^2}\right) 
$$

$$
f(y_i \mid x_i, \sigma_{y_i}, m, b) = \frac{1}{\sqrt{2\pi\sigma_{y_i}^2}} \exp\left(-\frac{\left[y_i - (mx_i + b)\right]^2}{2 \sigma_{y_i}^2}\right) 
$$

$$
f(y_i \mid x_i, \sigma_{y_i}, m, b) = \frac{1}{\sqrt{2\pi\sigma_{y_i}^2}} \exp\left(-\frac{\left[y_i - mx_i - b)\right]^2}{2 \sigma_{y_i}^2}\right) 
$$

<!-- Note that $$f(y_i \mid x_i, \sigma_{y_i}, m, b)$$ can be written as $$p(y_i \mid x_i, \sigma_{y_i}, m, b)$$, since it is a probability distribution; the probability of $$y_i$$ given the $$x_i$$ and model parameters.  -->


In linear regression with Gaussian distributed data, this becomes our maximum likelihood statistic. 


<!-- In maximum likelihood analysis, our f(y_i \mid x_i, \sigma_{y_i}, m, b) becomes our maximum likelihood statistic. 
becomes p(y_i \mid x_i, \sigma_{y_i}, m, b), as it is a probability function; the probability of $$y_i$$ given the $$x_i$$ and model parameters. -->


<!-- Notice that we also replaced f with p to match Hogg et al's paper. This helps to remind us that this function is representative of the probability of $$y_i$$ given the $$x_i$$ and model parameters. 
 -->


<!-- where $$ mx_i + b $$ represent the model estimates of $$y$$. I may refer to these as $$y_{model}$$ or $$ymodel$$. I may also refer to the y-axis data ($$y_i$$) as $$y_{data}$$ or $$ydata$$.  -->




# Maximum Likelihood
# The Likelihood (and Log-Likelihood) Statistic
The likelihood is the frequencey distribution for the observables evaluated at the observed data, $$y_i$$. It is also more commonly referred to as "the likelihood of the parameters", even though it is a function of both the data and the model parameters. The likelihood function is given by:

$$
\mathcal{L} = \prod^N_{i=1} p(y_i \mid x_i, \sigma_{y_i}, m, b)
$$

where $$ p(y_i \mid x_i, \sigma_{y_i}, m, b) $$ is the frequencey distribution (or the probability distribution we presented above) for Gaussian distributed data about a linear model. 
In Likelihood form:

$$
\mathcal{L} = \prod^N_{i=1} \frac{1}{\sqrt{2\pi\sigma_{y_i}^2}} \exp\left(-\frac{(y_i - mx_i - b)^2}{2 \sigma_{y_i}^2}\right) .
$$


When performing maximum likelihood estimation, the log-likelihood ($$\ln(\mathcal{L})$$) is used instead of the likelihood ($$\mathcal{L}$$). This is because the log-likelihood is easier to work with. The logarithmic product rule ($$ \log(xy) = \log(x) + \log(y) $$) allows products to be turned into sums, which are much easier to work with. 



$$
\ln(\mathcal{L}) = \sum^N_{i=1} p(y_i | x_i, \sigma_{y_i}, m, b)
$$


$$ \ln(\mathcal{L}) = -\frac{n}{2}\ln(2\pi)- n\ln \sigma - \sum \frac{(y_i-y_{model,i})^2}{2\sigma^2} $$

or

$$ 
\ln(\mathcal{L}) = -\frac{1}{2} \left[ n\ln(2\pi) + 2 n \ln(\sigma) + \sum \left(\frac{y_i-y_{model,i}}{\sigma}\right)^2 \right]
$$

Since we have technically set up the probability function to be dependent on $$\sigma_{y_i}$$, we should write the function as:

$$ 
\ln(\mathcal{L}) = -\frac{1}{2} \left[ n\ln(2\pi) + 2 n \ln(\sigma_{y_i}) + \sum \left(\frac{y_i-y_{model,i}}{\sigma_{y_i}}\right)^2 \right]
$$



# Bayes' Theorem
Here we write the most basic way to present Bayes' Theorem:


$$
p(\theta\mid D, I) = \frac{p(D \mid \theta, I) \ p(\theta \mid I)}{p(D\mid I)}
$$

where $$ p(\theta \mid D, I) $$ is the posterior probability, $$p(D \mid \theta, I)$$ is the likelihood (probability), $$ p(\theta \mid I) $$ is the prior probability distribution, and $$ p(D\mid I) $$ is a constant that arises from marginalizing the numerator over all parameters; it can be thought of as a normalization so that the posterior probability integrates (i.e., sums) to 1. That's all you really need to know about the denominator term. 

We use $$\theta$$ to represent all the model parameters. This includes all that are free to vary during the fit, both those you care about and those you do not. 
$I$ is short-hand for all the prior knowledge of the experiment, parameters and all, but holds no knowledge of the data (see prior section below since $$x_i$$ and $$\sigma_{y_i}$$ are NOT treated as data here). 
$$D$$ stands for data, which in our case is really only the $$y_1, y_2, ..., y_N$$. 

As stated in short by Hogg et al.: "the posterior probability distribution is the likelihood times the prior, properly normalized." 


## Prior
$I$ is short-hand for all the prior knowledge of the $$x_i$$ and the $$\sigma_{y_i}$$ and everything else about the problem. Hogg et al. notes that $$x_i$$ and $$\sigma_{y_i}$$ are consumed within the prior $$I$$ because they are NOT considered the data. They explain that there is a total asymmetry between $$x_i$$ and $$y_i$$ and the $$x_i$$ are considered to be part of the experimental design. They are inputs to an experiment that gets $$y_i$$ as its output. In data science practices, the $$X$$ matrix that holds the $$x_1, x_2, ..., x_N$$ data is called the features matrix and the $$Y$$ vector that holds the $$y_1, y_2, ..., y_N$$ data is called the response vector. This is because they are not treated as data, but features and a response of the experiment. Note that in Hogg et al, the so-called features matrix is $$\mathbf{A}$$ (see their Section 1) instead of $$\mathbf{X}$$, where they use $$\mathbf{X}$$ to represent the resulting parameters instead.


# Terms and Ideas

## Prior
$I$ is short-hand for all the prior knowledge of the $$x_i$$ and the $$\sigma_{y_i}$$ and everything else about the problem. Hogg et al. notes that $$x_i$$ and $$\sigma_{y_i}$$ are consumed within the prior $$I$$ because they are NOT considered the data. They explain that there is a total asymmetry between $$x_i$$ and $$y_i$$ and the $$x_i$$ are considered to be part of the experimental design. They are inputs to an experiment that gets $$y_i$$ as its output. In data science practices, the $$X$$ matrix that holds the $$x_1, x_2, ..., x_N$$ data is called the features matrix and the $$Y$$ vector that holds the $$y_1, y_2, ..., y_N$$ data is called the response vector. This is because they are not treated as data, but features and a response of the experiment. Note that in Hogg et al, the so-called features matrix is $$\mathbf{A}$$ (see their Section 1) instead of $$\mathbf{X}$$, where they use $$\mathbf{X}$$ to represent the resulting parameters instead.


<!-- ***marginalisation:***  -->
## Marginalisation
In probability it refers to "summing out" the probability of random variables given the joint probability distribution of other variables. It requires a measure on your data. Given by priors. Marginalization is a Bayesian technique. 








<!-- 

# Vector Form
$$
\begin{equation}
\qquad 
\mathbf{Y}=
\begin{bmatrix}
y_{1} \\
y_{2} \\
\vdots \\
y_{N}
\end{bmatrix}
\end{equation}
$$

$$
\begin{equation}
\qquad 
\mathbf{A}=
\begin{bmatrix}
1 & x_{1}\\ 
1 & x_{2}\\
\vdots \\ 
1 & x_{N}
\end{bmatrix}
\end{equation}
$$

$$
\begin{equation}
\mathbf{C}=
\begin{bmatrix}
\sigma_{y_1}^2 & 0 & \ldots & 0 \\ 
0 & \sigma_{y_2}^2 & \ldots & 0 \\
0 & 0 & \ddots & 0 \\ 
0 & 0 & \ldots & \sigma_{y_N}^2 
\end{bmatrix}
\end{equation}
$$


git add -A

git commit -m 'new'

git push origin master
 -->