---
layout: page
title: "Stability Measure for Minimum Variance Portfolios"
description: Cornell University, School of Operations Research and Information Engineering
img: assets/img/24.jpg
importance: 1
category: More to be added in the future
---
## Stability Measure for MVPs leveraging Marchenko-Pastur Theory and Eigenvalue Distributions
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/25.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
The Minimum Variance portfolio exhibits varying levels of stability and robustness. As a result, we suggest a theoretical approach to assessing its stability in relation to a Marchenko-Pastur derived random correlation matrix. 

This practical application is demonstrated using the S&P 400, the S&P 500, the S&P 600, and the Russell 1000. By analyzing historical market information from 2002 to 2021, we carry out an optimization process on the empirical correlation matrix eigenvalue distribution to establish the implied variance $$ν(t)$$ of the underlying data generation process. By tracking its temporal variation, $$Δν(t)$$, we present a Stability Measure for the Minimum Variance portfolio, thereby assisting researchers in evaluating shifts in estimation risk and managing rebalancing strategies.
## Introduction
The Minimum Variance portfolio, which consists of assets with the lowest risk, is situated on the Efficient Frontier and was initially recognized by Haugen and Baker (1991). Numerous researchers have since investigated it (Merton 1980, Chopra and Ziemba 2013), noting that its construction is subject to sampling errors. Klein and Bawa (1976) emphasize that such estimation risk has significant implications for optimal portfolio selection, resulting in asset weights that are unstable and subject to noise over time. Nonetheless, the Minimum Variance portfolio possesses a key attribute that enables the assessment of its stability: the covariance matrix is the sole unknown parameter, unlike the optimal portfolio, which necessitates an estimation of risky asset returns' mean, a more challenging task (Merton 1980). Despite its reduced estimation risk, the Minimum Variance portfolio still exhibits some instability. Therefore, we posit that alterations in implied process variance $$ν$$ offer a valuable gauge of stability over time. Our Stability Measure is founded on the notion of portfolio-specific stationarity, determined by tracking the temporal properties of a portfolio's empirical correlation matrix's signal-to-noise ratio.

The Stability Measure expands upon the foundational work of Marchenko and Pastur (1967), who derived an analytical form for the probability density function of a random covariance matrix's eigenvalue distribution. This matrix is composed of data elements that are independent, identically distributed random variables originating from a zero-mean process with finite variance. In instances where the data-generating process has unit variance, the covariance and correlation matrices are identical, rendering the Marchenko-Pastur eigenvalue distribution well-suited for calculating $$ν$$.

We demonstrate the effectiveness of the Stability Measure by analyzing historical market data and the corresponding empirical correlation matrix eigenvalue distribution, focusing on the S&P 400, S&P 500, S&P 600, and Russell 1000 from 2002 to 2021. Our findings illustrate the progression of $$ν(t)$$ over time $$Δν(t)$$, identifying periods and disruptions in portfolio-specific stationarity. These results carry implications for the overall effectiveness of portfolio management, methodological ramifications for researchers examining Modern Portfolio Theory, the Efficient Frontier, and estimation errors, as well as practical consequences for managing Minimum Variance index portfolios.

## Leveraging the Marchenko–Pastur Theorem for Assessing Stability in Portfolio Optimization

The Marchenko–Pastur theorem can be expressed as follows. Let $$𝑋$$ be a $$𝑇×𝑁$$ random matrix, where each elements $$𝑥_{𝑖𝑗}$$ are independent identically distributed (i.i.d.) random variables drawn from a zero-mean random process with finite variance $$\sigma^2$$. 

In the limit $$𝑁,𝑇→\infty$$, such that the ratio $$1<𝑞=\frac{T}{N}<\infty$$, matrix $$𝑀=\frac{1}{T} 𝑋^{'} 𝑋$$ has eigenvalues whose distribution converges to the analytic Marchenko–Pastur probability density function:

$$p(\lambda)=\left\{\begin{array}{rr}
\frac{q \sqrt{\left(\lambda_{+}-\lambda\right)\left(\lambda-\lambda_{-}\right)}}{2 \pi \lambda \sigma^{2}}, & \lambda \in\left[\lambda_{-}, \lambda_{+}\right] \\
0, & \lambda \in\left[\lambda_{-}, \lambda_{+}\right]
\end{array}\right.$$

where $$\lambda_{ \pm}=\sigma^{2}(1 \pm \sqrt{q})^{2}$$.

$$T$$ representing a series of consecutive trading days and as $$N$$ representing the number of components in an index portfolio such as the S&P 500. 

#### Marchenko–Pastur eigenvalue probability density function $$p(\lambda)$$
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/26.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
(a) Marchenko–Pastur eigenvalue probability density function for 𝜎^2=1 and a range of values of the quality parameter q. 
(b) as (a) but for fixed 𝑞=1.5 and a range of values of 𝜎^2. 
</div>
The figure on the left demonstrates the probability density function for various values of $$q$$ with a fixed $$σ^2=1$$. As $$q$$ approaches a larger value, the eigenvalue distribution becomes increasingly narrow, as depicted in the image, which corresponds to a distribution where all eigenvalues are $$1$$. In the context of population dynamics, this is equivalent to the correlation matrix converging towards the identity matrix. Referring to the left figure, $$q$$ ($$=T/N$$) is adjusted by altering $$T$$, while keeping $$N$$ constant. In the analysis of actual stock data, unless specified otherwise, $$q = 1.5$$ will be employed. The figure on the right illustrates the impact of modifying the process variance with a fixed $$q = 1.5$$.

#### Separate eigenvalues for ‘signal’ from those for ‘noise’
The Marchenko–Pastur is a good fit for the distribution of those eigenvalues associated with noise, distinct from those associated with signal. It facilitates a threshold separation between those eigenvalues associated with noise and those associated with signal:

$$\lambda_{-}<\lambda<\lambda_{+}$$ where $$\lambda_{ \pm}=\sigma^{2}(1 \pm \sqrt{q})^{2}$$

Eigenvalues that fall outside this range can be considered as signal eigenvalues, while those inside the range are associated with noise. Financial data matrices generally have very low signal-to-noise ratios rendering them potentially suitable for comparison with Marchenko–Pastur derived matrices.

Apply this threshold to empirical data:
1. Standardize the $$𝑇×𝑁$$ empirical data so that each column of the data matrix has zero mean and unit variance.
2. Perform eigen-decomposition on the column-standardized empirical data matrix.
3. Apply a a Gaussian kernel density fit to those eigenvalues that lie within the Marchenko–Pastur boundaries for noise, i.e., $$\lambda_{-}<\lambda<\lambda_{+}$$ where $$\lambda_{ \pm}=\sigma^{2}(1 \pm \sqrt{q})^{2}$$
4. Fit with the analytic Marchenko-Pastur probability density function (the benchmark) to get the the implied process variance $$𝜈=𝜎_{𝑜𝑝𝑡}^2$$ by minimises the distance between the analytic pdf and the empirical KDE.

#### M–P pdf vs. Gaussian KDE to simulated random data with no signal 
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/27.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
In the case of random data devoid of any signal, as illustrated in the above left and right figures, the optimization occurs for $$σ_{opt}^2=1$$. This is expected since we are dealing with purely random (no signal) data generated from a stationary zero-mean parent process with unit variance (in the case of Gaussian and Uniform generated data). The left figure displays the results of generating data ($$N = 500$$, $$T = 750$$, thus $$q = 1.5$$) from four distinct probability distributions: a standard normal distribution; a uniform distribution with zero mean and unit variance, a Cauchy distribution centered at zero with $$\lambda = 1$$, and a $$t$$-distribution with one degree of freedom. The latter two serve as examples of distributions exhibiting heavier tails than Gaussian processes. The primary distinction between the left and right figures lies in the increase of $$q$$ to $$5$$ in the right figure. 

A notable observation from the left figure, i.e., for $$q = 1.5$$, is that the process appears considerably more agnostic to the source data-generating process. As we transition to the right figure with $$q = 5$$, it becomes evident that the process is not suitable for Cauchy and t-distribution sourced data. This informs the selection of q when working with market data and offers the added benefit of simplifying the calibration of our stability management system. It is crucial to note that values of $$q ≈ 1$$ may yield erroneous behavior, but $$q = 1.5$$ generates robust results while enabling us to capitalize on practical design advantages.

## Simulate Random data (with signal) 
Aim: Generate a correlation matrix for data containing both noise and signal to simulate the actual market data behavior.

1.Generate a $$𝑁×𝑓$$ factor matrix $$𝐹$$ with elements from a standard Gaussian distribution: 

$$𝐹_{𝑖𝑗}∼𝑁(0,1)$$, where $$𝑖=1,2,...,𝑁$$; $$j=1,2,...,𝑓$$. $$𝑓$$ is the number of channels (we may think of channels as factors) into which we wish to inject the signal and 𝑁 is the number of assets ($$𝑓<𝑁$$). 
2.Generate a covariance matrix $$𝐹𝐹^{'}$$, where $$𝐹^{'}$$ is the the transpose of $$𝐹$$.

3.Generate a $$𝑁×𝑁$$ diagonal matrix $$𝐷$$ with elements from a Uniform distribution: $$𝐷_{𝑖𝑖}∼𝑈(0,1)$$, for $$𝑖=1,2,...,𝑁$$.

4.Generate the $$𝑁×𝑁$$ signal matrix $$𝑆$$ (full-rank): $$𝑆=𝐹𝐹^{'}+𝐷$$.

5.Generate a random covariance matrix $$𝑄$$ (populated from standard Gaussian).

6.Generate the noise-with-signal-embedded covariance matrix $$R$$ : $$𝑅=\alpha𝑄+(1−\alpha)𝑆$$, we use a very weak signal to simulate financial data by setting $$\alpha=0.995$$.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/28.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Simulation under the case where the signal has been injected into 10% of the channels (𝑓 is 10% of 𝑁) i.e., 𝑁=300, 𝑓=30, we use a very weak signal by seting 𝛼=0.995. Also, 𝑞 is set to be 1.5.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/29.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Simulation under the case where the signal has been injected into 20% of the channels (𝑓 is 20% of 𝑁) i.e., 𝑁=300, 𝑓=60, we use a very weak signal by seting 𝛼=0.995. Also, 𝑞 is set to be 1.5.
</div>

#### KDE of the eigenvalue distribution of covariance matrix $$R$$
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/30.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
The figure on the left demonstrates the outcome of applying the Kernel Density Estimation (KDE) to the discrete eigenvalue distribution of the corresponding correlation matrix, in cases where the signal has been incorporated into 10% of the channels ($$f$$ is 10% of $$N$$). The distribution exhibits a distinctive pattern, consisting of a bulk of eigenvalues separated from a series of discrete eigenvalues representing the signal introduced as factors at the beginning of the process. The figure on the right presents the eigenvalue distribution for a case analogous to the one in the left figure, with the exception that noise has been incorporated into 20% of the channels.

The figure on the left yields a value of $$ν = σ_{opt}^2 = 0.675$$, which can be interpreted as a measure of the signal-to-noise ratio in the original data. A lower value indicates a higher signal-to-noise ratio in the dataset. The value of $$ν$$ is bounded above by $$1$$, as the optimization is performed relative to purely random noise generated by a zero-mean, unit variance process. An optimization resulting in a value of $$ν = 1$$ would essentially signify that the observed data contains no signal and is purely noise. In the case of the figure on the right, the increased signal levels produce a lower optimum parameter value of $$ν = σ_{opt}^2 = 0.504$$, in line with the higher signal-to-noise ratio.

## Stationarity
Suppose the underlying data-generating process is Gaussian $$N(\mu,\sigma^2)$$. When we refer to a period of stationarity, we mean that this process remains the underlying data generating process throughout that period of time, with fixed $$\mu$$ and fixed $$\sigma^2$$.

Identifying breaks in stationarity is crucial, as any statistical analysis across non-stationary periods may be inaccurate. Detecting these breaks allows for improved predictive model efficacy by mitigating potential negative impacts.

Our Stability Measure is therefore based on the concept of portfolio-specific stationarity, and determined by monitoring the temporal properties of the signal-to-noise ratio of a portfolio’s empirical correlation matrix, i.e. $$\Delta𝜈(𝑡)$$. It has implication in measuring of stability for the Minimum Variance portfolio over time and thereby helping researchers measure changes to estimation risk and manage rebalancing regimes.

Smyth and Broby (2022) argue that a period of stationarity is typified by a distribution of $\Delta𝜈(𝑡)$ centred on zero and having a spread of typically ±5%.

#### Periods of stationarity and breaks in stationarity over historical time 
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/31.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
The manifestation of stationarity is illustrated in Figure (a) on the right, where clear fluctuations (sampling effects) are observed. However, these fluctuations are confined within a consistent vertical band, indicative of stationarity and exhibiting a bandwidth typical of this specific scenario ($$N(0, 1)$$ and $$q = 1.5$$). Similar effects are displayed in the other frames of the right figure for various known distributions. This connection between our stability measure and stationarity is vital. Stationarity, or its disruptions, materialize through the magnitude of fluctuations in $$ν(t)$$. Figure (a-d) on the right demonstrates examples of behavior for defined statistical processes, which are stationary over the entire time period. In contrast, Figure (a-d) on the left illustrates empirical financial data.

To offer an overview that enables a comparison between actual market data analysis and simulated data from known stationary processes, we include Figure (a-d) on both the left and the right. Each frame depicts the weekly percentage change in $$ν$$. The left figure represents the backtest outcomes for four market indices, while the right figure shows simulations using known stationary processes. The most evident distinction between the figures is the pulsing behavior observed over time for the market data in the left figure. This pulsing effect, entirely absent in the perpetually stationary processes of the right figure, conveys periods of stationarity and breaks in stationarity over time.

## Stability measure with the actual market data
Note:
- The methodology relies on the correlation matrix and its eigen-decomposition, without referencing portfolio weights.
- We do not employ the correlation matrix of one index portfolio to predict the stability of another index portfolio's Minimum Variance portfolio. 
- A short stability monitoring window of one week, or the weekly percentage change in $$𝝂$$, is adopted for our analysis.
- The results are valid for the correlations that exist and evolve solely within the core subset of stocks consistently present throughout the 2002–2021 period. In the case of the S&P 500, this corresponds to 389 stocks.
- A step size of one day is utilized as the monitoring frequency for the rolling window when analyzing daily returns data.
- The parameter $$𝑞$$ is set to 1.5 in our study.

#### Stability measure $$𝛎(𝐭)$$ from 2006 to 2021
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/32.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Figure on the left demonstrates the evolution of $$ν$$ (the signal-to-noise ratio of the empirical correlation matrix) over time for the S&P 400, 500, 600, and the Russell 1000 indices during the period from the beginning of 2006 to the end of 2021. This figure exhibits several intriguing features. There are noticeable similarities and differences across indices. As highlighted earlier, the significant events of 2008 and 2020 are clearly discernible across all indices, evidenced by substantial, almost instantaneous changes in $$ν$$.

Figure on the right illustrates the distribution of $$ν$$ for each index under consideration over the same time period as in Figure on the left. This image is characterized by discrete poles around which a spread of values is observed. Each pole signifies the central value of a period of stationarity, and thus, Minimum Variance portfolio stability. Conversely, transitions between poles indicate breaks in stationarity.

#### Distribution of $$𝚫𝛎(𝐭)$$ with the S&P 400 index
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/33.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
Figure on the left provides a more detailed view by focusing on the S&P 400 index and selecting three regions of stationarity. Color-coding is employed to link the periods from the left to the right frames. It is instructive to examine the changes in $$ν$$ during each of the periods identified in this image.

To this end, Figure on the right displays the distribution of the weekly percentage change in ν. For each of the regions identified as periods of stationarity, the modal weekly change is predominantly zero. Moreover, in each of these regions, the range of values is confined within ±4% (the green zone has a single anomalous daily value that can be identified as the spike in Figure on the left, causing the scale on the x-axis to broaden). The fourth frame of Figure on the right contains the distribution of values for all other regions combined. The mean weekly percentage change for all other regions is still zero, albeit less overwhelmingly so. Indeed, excluding the spike at zero for each frame results in values for the mean and variance of the distributions shown, which are twice as large for all other regions as for any of the color-coded regions, whose first and second moments are quite similar.

## Conclusion

We have introduced a mechanism for assessing the stability of the Minimum Variance portfolio on the efficient frontier, which we refer to as the Stability Measure. This measure is grounded in Marchenko–Pastur theory and focuses on the distribution of eigenvalues associated with noise, as opposed to those related to the signal. The Stability Measure emerges as a result of an optimization process that aims to maximize the similarity between the discrete distribution of noise-related eigenvalues in an empirical correlation matrix and a benchmark analytic Marchenko–Pastur probability density function.

We apply the Stability Measure to several Minimum Variance portfolios derived from key US equity indices. Our primary finding reveals that the stability of a Minimum Variance index portfolio can be determined through the empirical correlation matrix of the core stocks comprising that specific index. In this context, portfolio stability can be considered analogous to stationarity in a portfolio-specific data-generating process. The ability to effectively monitor stability for a core subset of stocks enables implementation at higher frequencies than typically associated with rebalancing. By detecting changes in portfolio stability or identifying breaks in the stationarity of a portfolio-specific data-generating process, our stability monitoring approach can serve as an indicator for the need to adjust the rebalancing schedule.

## References

- Chopra, V.K. and Ziemba, W.T., The effect of errors in means, variances, and covariances on optimal portfolio choice. In Hand- book of the Fundamentals of Financial Decision Making: Part I, edited by W. Y. Ziemba, pp. 365–373, 2013 (World Scientific Publishing).

- Haugen, R.A. and Baker, N.L., The efficient market inefficiency of capitalization–weighted stock portfolios. J. Portf. Manag., 1991, 17(3), 35–40.

- Klein, R.W. and Bawa, V.S., The effect of estimation risk on optimal portfolio choice. J. Financ. Econ., 1976, 3(3), 215–231

- Marchenko, V.A. and Pastur, L.A., Distribution of eigenvalues for some sets of random matrices. Math. USSR-Sbornik, 1967, 1(4), 457–483.

- Merton, R.C., On estimating the expected return on the market: An exploratory investigation. J. Financ. Econ., 1980, 8(4), 323– 361.
