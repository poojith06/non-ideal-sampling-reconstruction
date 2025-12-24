# Reconstruction of Band-Limited Signals Under Sampling-Time Jitter

## Overview

In ideal Nyquist sampling, a band-limited continuous-time signal can be perfectly reconstructed when samples are taken uniformly above the Nyquist rate. In practice, however, sampling often deviates from ideal assumptions due to hardware imperfections such as **sampling-time jitter**. These non-idealities introduce distortion and degrade reconstruction accuracy.

This project develops and evaluates reconstruction techniques for band-limited signals sampled under **non-ideal sampling-time jitter**, assuming that the jitter is known. The performance of the reconstruction method is quantified using multiple test signals and analyzed as a function of jitter magnitude.

---

## Problem Statement

We are familiar with the Nyquist sampling criterion for band-limited signals and their perfect reconstruction under ideal conditions. In this problem, we address complexities that arise due to **non-ideal sampling conditions** which may occur in practice.

Let the signal of interest be a continuous-time band-limited signal \( x(t) \), sampled above the Nyquist rate with sampling interval \( T_s \). The ideal discrete-time samples are given by:

\[
x[n] = x(nT_s)
\]

### Non-Ideal Sampling Scenario: Sampling-Time Jitter

In this scenario, the \(n\)-th sample is not taken exactly at time \( nT_s \), but at a perturbed time instant due to sampling-time jitter. The observed samples are:

\[
\hat{x}[n] = x(nT_s + k_n \Delta)
\]

where:
- \( \Delta = \frac{T_s}{10} \),
- \( k_n \) is an integer-valued random variable,
- \( k_n \) is equally likely to take any integer value in the range \([-K, K]\),
- \( 1 \leq K \leq 4 \).

The deviation \( k_n \Delta \) is **known**, but varies randomly across samples.

### Objective

For the above non-ideal sampling scenario, the objective is to:

- Develop a method to estimate the ideal samples \( x[n] \) from the jittered samples \( \hat{x}[n] \),
- Justify the proposed method through analysis,
- Demonstrate the reconstruction using **at least three distinct band-limited signals**,
- Quantify the reconstruction performance as a function of the jitter bound \( K \).

---

## Methodology

For band-limited signals, ideal reconstruction is governed by sinc interpolation:

\[
x(t) = \sum_{m=-\infty}^{\infty} x[m] \, \text{sinc}\left(\frac{t}{T_s} - m\right)
\]

Evaluating this expression at jittered sampling instants leads to a linear relationship between jittered samples and ideal samples:

\[
\hat{\mathbf{x}} = \mathbf{H}\mathbf{x}
\]

where the matrix \( \mathbf{H} \) contains sinc-based weights determined by the known sampling-time deviations.

To recover the ideal samples, the inverse problem is solved using a least-squares approach:

\[
\hat{\mathbf{x}}_{\text{est}} = \mathbf{H}^{\dagger}\hat{\mathbf{x}}
\]

where \( \mathbf{H}^{\dagger} \) denotes the Moore–Penrose pseudo-inverse.

---

## Test Signals

The reconstruction method is demonstrated using three distinct band-limited signals:

1. A single low-frequency sinusoid  
2. A multi-tone band-limited signal  
3. A shifted sinc signal  

All signals satisfy the Nyquist sampling criterion.

---

## Performance Metric

Reconstruction accuracy is quantified using the **Mean Squared Error (MSE)**:

MSE = (1 / N) * Σ_{n=0}^{N−1} [ x[n] − x_est[n] ]²

The MSE is evaluated as a function of the jitter bound \( K \).

---

## Results

The experimental results include:

- Reconstruction of three band-limited signals from jittered samples
- Mean Squared Error as a function of jitter level \( K \)

Key observations:
- Accurate reconstruction is achieved for small jitter levels
- Reconstruction error increases monotonically with increasing \( K \)
- The results are consistent with theoretical expectations

---

## Tools and Environment

- MATLAB
- Sinc interpolation
- Least-squares (pseudo-inverse) reconstruction

---

## Conclusion

This project demonstrates that sampling-time jitter can be effectively compensated when the jitter is known. By modeling jitter-induced distortions using sinc interpolation and solving the resulting inverse problem, accurate reconstruction of band-limited signals is achievable. The study also highlights the degradation in reconstruction performance as jitter magnitude increases.

---
