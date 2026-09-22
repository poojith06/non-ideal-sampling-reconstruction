# Reconstruction of Band-Limited Signals Under Sampling-Time Jitter

## Overview

In ideal Nyquist sampling, a band-limited continuous-time signal can be perfectly reconstructed when samples are taken uniformly above the Nyquist rate. In practice, however, sampling often deviates from ideal assumptions due to hardware imperfections such as **sampling-time jitter**. These non-idealities introduce distortion and degrade reconstruction accuracy.

This project develops and evaluates reconstruction techniques for band-limited signals sampled under **non-ideal sampling-time jitter**, assuming that the jitter is known. The performance of the reconstruction method is quantified using multiple test signals and analyzed as a function of jitter magnitude.

---

## Problem Statement

We are familiar with the Nyquist sampling criterion for band-limited signals and their perfect reconstruction under ideal conditions. In this problem, we address complexities that arise due to **non-ideal sampling conditions** which may occur in practice.

Let the signal of interest be a continuous-time band-limited signal ( x(t) ), sampled above the Nyquist rate with sampling interval ( Ts ). The ideal discrete-time samples are given by:

x[n] = x(nTs)

### Non-Ideal Sampling Scenario: Sampling-Time Jitter

In this scenario, the n-th sample is not taken exactly at time ( nTs ), but at a perturbed time instant due to sampling-time jitter. The observed samples are:

x_hat[n] = x(n·Ts + k_n·Δ)

where:
- Δ = Ts / 10
- k_n is an integer-valued random variable
- k_n is equally likely to take any integer value in the range [−K, K]
- 1 ≤ K ≤ 4

The deviation k_n·Δ is known, but varies randomly across samples.

### Objective

For the above non-ideal sampling scenario, the objective is to:

- Develop a method to estimate the ideal uniform samples x[n] from the jittered samples x_hat[n],
- Justify the proposed method through analysis,
- Demonstrate the reconstruction using **at least three distinct band-limited signals**,
- Quantify the reconstruction performance as a function of the jitter bound \( K \).

---

## Proposed Reconstruction Method

For band-limited signals, ideal reconstruction is governed by sinc interpolation:

x(t) = sum_{m = −∞}^{∞} x[m] · sinc(t / Ts − m)

Due to sampling-time jitter, samples are obtained at perturbed time instants. Evaluating the sinc interpolation formula at these jittered instants leads to a linear relationship between the jittered samples and the ideal uniform samples:

x_hat = H · x

Here, x_hat represents the vector of jittered samples, x represents the vector of ideal uniform samples, and H is a matrix whose elements are sinc-based weights determined by the known sampling-time deviations. Each entry of H captures the contribution of an ideal sample to a jittered sample based on the corresponding timing offset.

To recover the ideal samples from the jittered measurements, the resulting inverse problem is solved using a inverse of the matrix H:

x_est = H† · x_hat

where H† denotes the pseudo-inverse of the matrix H. This approach compensates for the sample coupling introduced by sampling-time jitter and provides an estimate of the original uniform samples.

---

## Test Signals

The reconstruction method is demonstrated using three distinct band-limited signals:

1. A single low-frequency sinusoid  
2. A multi-tone band-limited signal  
3. A shifted sinc signal  

All signals satisfy the Nyquist sampling criterion.

---

## Performance Evaluation

Reconstruction accuracy is quantified using the **Mean Squared Error (MSE)**:

MSE = (1 / N) * Σ_{n=0}^{N−1} [ x[n] − x_est[n] ]²

The MSE is evaluated as a function of the jitter bound \( K \).

---

## Results

The experimental results include:

- Reconstruction of three band-limited signals from jittered samples
- Mean Squared Error as a function of jitter level \( K \)
- Accurate reconstruction is achieved for small jitter levels

---

## Tools and Environment

- MATLAB
- Sinc interpolation
- Least-squares (pseudo-inverse) reconstruction

---

## Conclusion

This project demonstrates that sampling-time jitter can be effectively compensated when the jitter is known. By modeling jitter-induced distortions using sinc interpolation and solving the resulting inverse problem, accurate reconstruction of band-limited signals is achievable. The study also highlights the degradation in reconstruction performance as jitter magnitude increases.

---
