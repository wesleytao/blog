---
title: "Time Series"
author: "Wesley_Tao"
date: "2018.8.15"
output: html_document
---

# waht is stationary and why do we need it?
Strongly stationary Definition:
$$F_X(x_{t_1+\tau},...,x_{t_k+\tau})=F_X(x_{t_1},...,x_{t_k}) \space for \space all \space k \space ,\tau $$
This means the joint distribution of any length of the sequences is the same if we shift the window by any time gap.

Weakly Stationary Definition:
$$ (i) \, E[X_t]=\mu $$
$$ (ii) \, Var(X_t)=\sigma^2 $$

$$(iii) \, Cov(X_t,X_{t+h})=f(h)$$

This means there are some underlying data generating process of $X_t$ for all period.

The reason why we need stationary is we need to analyze certain behaviour of the target value, if the data generating process change across time, we are not able to clarify the dependency between the variables. And theoretically speaking, we are unable to do statistical inference using the Low of Large Number or Central limit therom.
