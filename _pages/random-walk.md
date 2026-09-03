---
permalink: /notes/random-walk/
title: "Random Walk for IMUs"
author_profile: true
---

A sequence of IMU measurements is disturbed by a white noise sequence (uncorrelated random variables with zero mean and finite variance) with some bias. If we are integrating the IMUs to determine position and heading, we should understand the way the noise propagates to these.
If we have multiple IMU and average the measurements, we expect the error be reduced by some amount. To determine the expected reduction in error from averaging multiple IMUs, we can look at how the position and heading is affected by this noise. For this simple analysis, we will assume the position and orientation of each IMU are the same.

### Angle Random Walk for 1 Gyroscope (no bias)

Consider the angle obtained by integrating the gyroscope over a period of $$t$$ seconds given by

$$
\begin{aligned}
\hat{\theta}^{(1)} &= \int_0^t \dot{\theta}(\tau) + \epsilon(\tau) d\tau \\
&= \theta + \int_0^t \epsilon(\tau) d\tau
\end{aligned}
$$

where $$\theta$$ is the true heading and $$\epsilon(\tau)$$ is the white noise signal. Let $$X_i$$ be the $$i$$th random variable in a white noise sequence. Since the sequence is uncorrelated with zero mean and finite variance, $$\mathsf{E}[X_i] = \mathsf{E}[X] = 0$$, $$\mathsf{Var}[X_i] = \mathsf{Var}[X] = \sigma^2$$, and $$\mathsf{Cov}[X_i,X_j]=0$$ for all $$i \neq j$$. Consider the white noise signal, $$\epsilon(t)$$, integrated over a period of, $$t$$, seconds given by

$$
\int_0^t \epsilon(\tau) d\tau = T_s \sum_{i=1}^n X_i
$$

where $$n$$ is the number of samples obtained during the period and $$T_s$$ is the sampling time such that $$t = nT_s$$. Noting that $$\mathsf{E}[A + B] = \mathsf{E}[A] + \mathsf{E}[B]$$ where $$A$$ and $$B$$ are random variables and the expected value of a scalar is a scalar, the expected value of the heading after a period of $$t$$ seconds is given by

$$
\begin{aligned}
\mathsf{E}[\hat{\theta}^{(1)}] &= \mathsf{E} \left[ \theta + \int_0^t \epsilon(\tau) d\tau \right]\\
&= \mathsf{E}[\theta] + \mathsf{E} \left[ T_s \sum_{i=1}^n X_i \right] \\
&= \theta + T_s \sum_{i=1}^n \mathsf{E} \left[ X_i \right] \\
&= \theta.
\end{aligned}
$$

Noting that

$$
\mathsf{Var}[\alpha + X] = \mathsf{Var}[X]
$$

$$
\mathsf{Var}\left[\sum_{i=1}^n \alpha_i X_i\right]
= \sum_{i=1}^n \alpha_i^2 \mathsf{Var}[X_i]
+ \sum_{i \neq j} \alpha_i \alpha_j \mathsf{Cov}[X_i,X_j]
$$

where $$\alpha$$ is a scalar, then the variance of the heading after a period of $$t$$ seconds is given by

$$
\begin{aligned}
\mathsf{Var}[\hat{\theta}^{(1)}] &= \mathsf{Var} \left[\theta + \int_0^t \epsilon(\tau) d\tau \right] \\
&= \mathsf{Var} \left[ \sum_{i=1}^n T_s X_i \right] \\
&= \sum_{i=1}^n T_s^2 \mathsf{Var} \left[ X_i \right] + \sum_{i \neq j} T_s^2 \mathsf{Cov}[X_i,X_j] \\
&= T_s^2 \sum_{i=1}^n \mathsf{Var}[X_i] \\
&= T_s^2 \sum_{i=1}^n \sigma^2 \\
&= T_s^2 n \sigma^2 \\
&= T_s t \sigma^2
\end{aligned}
$$

where $$\sigma$$ is the standard deviation of the white noise signal. Note $$\mathsf{Cov}[X_i,X_j] = 0$$ where $$i\neq j$$ since the random variables are uncorrelated. Therefore, the noise introduces a first order error into the integrated signal that grows with time with zero mean and standard deviation given by

$$
\sigma_{\theta}^{(1)}(t) = \sigma \sqrt{T_s t}
$$

where $$\sigma_{\theta}^{(1)}(t)$$ is the standard deviation at time $$t$$ of the heading obtained by integrating a single gyroscope.

### Angle Random Walk for N Gyroscopes (no bias)

Now, consider multiple gyroscopes such that each gyroscope is located in the same position and orientation. Then, the angle obtained by averaging the measurements together is given by

$$
\begin{aligned}
\hat{\theta}^{(N)} &= \int_0^t \sum_{i=1}^N \frac{\dot{\theta}_i(\tau) + \epsilon_i(\tau)}{N} d\tau \\
&= \theta + \frac{1}{N} \int_0^t \sum_{i=1}^N \epsilon_i(\tau) d\tau \\
&= \theta + \frac{1}{N} \int_0^t \epsilon' (\tau) d \tau
\end{aligned}
$$

where $$N$$ is the number of gyroscopes being averaged together and $$\epsilon' = \sum_{i=1}^N \epsilon_i (\tau)$$. The variance for integrating the average signal is then given by

$$
\begin{aligned}
\mathsf{Var}\left[ \frac{1}{N} \int_0^t \epsilon' (\tau) d \tau \right] &= \mathsf{Var}\left[ \frac{T_s}{N} \sum_{i=1}^n Y_i \right] \\
&= \frac{T_s^2}{N^2} \sum_{i=1}^n \mathsf{Var}\left[ Y_i \right] \\
&= \frac{T_s^2}{N^2} \sum_{i=1}^n \sum_{j=1}^N \mathsf{Var}\left[ X_{i}^{(j)} \right] \\
&= \frac{T_s^2}{N^2} \sum_{i=1}^n \sum_{j=1}^N \sigma^2 \\
&= \frac{T_s^2}{N^2} nN\sigma^2 \\
&= \frac{T_s}{N}t\sigma^2
\end{aligned}
$$

where $$Y_i = \sum_{j=1}^N X_i^{(j)}$$ where $$X_i^{(j)}$$ is the $$i$$th random variable of the white noise sequence for the $$j$$th gyroscope. Therefore, the standard deviation of the noise introduced to the error for $$N$$ gyroscopes is given by

$$
\sigma_{\theta}^{(N)}(t) = \sigma \sqrt{\frac{T_s}{N}t}
$$

where $$\sigma_{\theta}^{(N)}(t)$$ is the variance at time $$t$$ by integrating the average measurements of $$N$$ gyroscopes. Therefore, we have

$$
\frac{\sigma_{\theta}^{(1)}(t)}{\sigma_{\theta}^{(N)}(t)} = \sqrt{N}
$$

where $$N$$ is the total number of gyroscopes such that each gyroscope has same error characteristics. Therefore, the variance for $$N$$ gyroscopes is linearly proportional to the variance of a single gyroscope with proportionality coefficient $$1/N$$.

### Position Random Walk for 1 Accelerometer (no bias)

Now, consider the position, $$x$$ obtained by integrating the accelerometer over a period of $$t$$ seconds by

$$
\begin{aligned}
\hat{x}^{(1)} &= \int_0^t\int_0^t \dot{v}(\tau) + \epsilon(\tau) d\tau d\tau \\
&= x + \int_0^t\int_0^t \epsilon(\tau) d\tau d\tau
\end{aligned}
$$

where $$x$$ is the true position and $$\epsilon(\tau)$$ is the white noise signal. Then, the white noise signal, $$\epsilon(\tau)$$, integrated twice over a period of, $$t$$, seconds is given by

$$
\begin{aligned}
\int_0^t\int_0^t \epsilon(\tau) d\tau d\tau &= T_s^2 \sum_{i=1}^{n} \sum_{j=1}^{i}X_i \\
&= T_s^2 [X_1 + (X_1 + X_2) + \cdots] \\
&= T_s^2 \sum_{i=1}^n (n-i+1)X_i
\end{aligned}
$$

where $$n$$ is the number of samples. The expected value of the position after a period of $$t$$ seconds is given by

$$
\begin{aligned}
\mathsf{E}[\hat{x}^{(1)}] &= \mathsf{E} \left[ x + \int_0^t\int_0^t \epsilon(\tau) d\tau d\tau \right]\\
&= \mathsf{E}[x] + \mathsf{E} \left[T_s^2 \sum_{i=1}^n (n-i+1) X_i \right] \\
&= x + T_s^2 \sum_{i=1}^n (n-i+1) \mathsf{E} \left[X_i \right] \\
&= x.
\end{aligned}
$$

The variance of the position after a period of $$t$$ seconds is given by

$$
\begin{aligned}
\mathsf{Var}[\hat{x}^{(1)}] &= \mathsf{Var} \left[x+ \int_0^t\int_0^t \epsilon(\tau) d\tau d\tau \right] \\
&= \mathsf{Var} \left[ T_s^2 \sum_{i=1}^n (n-i+1)X_i \right] \\
&= T_s^4 \sum_{i=1}^n (n-i+1)^2 \mathsf{Var} \left[ X_i \right] \\
&= \sigma^2 T_s^4 \sum_{i=1}^n (n-i+1)^2 \\
&= \sigma^2 T_s^4 \frac{n(n+1)(2n+1)}{6} \\
&= \sigma^2(\frac{T_st^3}{3} + \frac{T_s^2t^2}{2} + \frac{T_s^3t}{6}) \\
&\approx \sigma^2\frac{T_st^3}{3}
\end{aligned}
$$

where the sampling frequency, $$1/T_s$$, is assumed to be large. Note that $$\sum_{i=1}^n (n-i+1)^2$$ is equivalent to the sum of the first $$n$$ positive squared integers. Therefore, the noise introduced to the signal is second order that grows with time with zero mean and standard deviation given by

$$
\sigma_x^{(1)}(t) = \sigma t^{3/2} \sqrt{\frac{T_s}{3}}
$$

where $$\sigma_x^{(1)}(t)$$ is the standard deviation at time $$t$$ of the position obtained by integrating a single accelerometer.

### Position Random Walk for N Accelerometers (no bias)

Consider multiple accelerometers such that each accelerometer is located with identical position and orientation. Then, the position obtained by averaging the measurements together is given by

$$
\begin{aligned}
\hat{x}^{(N)} &= \int_0^t \int_0^t \sum_{i=1}^N \frac{ \dot{v}_i(\tau) + \epsilon_i(\tau)}{N} d\tau d\tau \\
&= x + \frac{1}{N} \int_0^t \int_0^t \sum_{i=1}^N\epsilon_i(\tau) d\tau d\tau \\
&= x + \frac{1}{N} \int_0^t \int_0^t \epsilon'(\tau) d\tau d\tau
\end{aligned}
$$

where $$N$$ is the number of accelerometers being average together and $$\epsilon'(\tau) = \sum_{i=1}^N\epsilon_i(\tau)$$. The variance of the signal is then given by

$$
\begin{aligned}
\mathsf{Var}\left[\frac{1}{N} \int_0^t \int_0^t \epsilon'(\tau) d\tau d\tau \right] &= \mathsf{Var}\left[ \frac{1}{N} T_s^2 \sum_{i=1}^n (n-i+1)Y_i \right] \\
&= \frac{T_s^4}{N^2} \sum_{i=1}^n(n-i+1)^2 \mathsf{Var}\left[Y_i\right] \\
&= \frac{T_s^4}{N^2} \sum_{i=1}^n(n-i+1)^2 \sum_{j=1}^N \mathsf{Var}\left[X_i^{(j)}\right] \\
&= \frac{T_s^4}{N^2} \sum_{i=1}^n(n-i+1)^2 \sum_{j=1}^N \sigma^2 \\
&= \frac{1}{N} \sigma^2 T_s^4 \sum_{i=1}^n(n-i+1)^2 \\
&= \frac{\sigma^2 T_s t^3}{3N}
\end{aligned}
$$

where $$Y_i = \sum_{j=1}^N X_i^{(j)}$$ where $$X_i^{(j)}$$ is the $$i$$th random variable of the white noise sequence for the $$j$$th accelerometer. Therefore, the noise introduced to the signal is second order that grows with time with zero mean and standard deviation given by

$$
\sigma_x^{(N)}(t) = \sigma t^{3/2} \sqrt{\frac{T_s}{3}}
$$

where $$\sigma_x^{(N)}(t)$$ is the standard deviation at time $$t$$ of the position obtained by integrating $$N$$ accelerometers. Therefore, we have

$$
\frac{\sigma_x^{(1)}(t)}{\sigma_x^{(N)}(t)} = N
$$

where $$N$$ is the total number of accelerometers such that each accelerometer has same error characteristics. Therefore, the variance for $$N$$ accelerometers is quadratically proportional to the variance of a single accelerometer with proportionality coefficient $$1/N^2$$.