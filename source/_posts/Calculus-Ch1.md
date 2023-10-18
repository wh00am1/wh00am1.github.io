---
title: Calculus::Ch1&Ch2
date: 2023-10-18 18:02:05
tags:
	- calculus
	- notes
---

## Basics
<!-- more -->
### Trigonometric
- $csc=1/sin$
- $sec=1/cos$
- $cot=1/tan$
## Limits&Contiuity
### Definition
- epsilon-delta
- to proof $\lim_{x \to x_0} f(x)=L$ ,
- write if , for every number epsilon>0, exists a corresponding delta>0 that :
- $0 < |x-x_0| < \delta \quad \Rightarrow  |f(x)-L|< \epsilon$
- find epsilon and delta by calculation
### One-sided
#### # approachs from either left or right
### Contiuity
Has the following situation of discontinuous:

- Jumped
	- The funcion jumps and continue from the destination
	- e.g. `The greatest integer function`
- Removable
	- The function is not defined on the point
	- e.g. $f(x)=1/x$
- Infinite
	- AKA. Essential
	- The function has a vertical asymptote(漸近線)
### Infinity
- definition
	- write :
	- $$lim_{x \to \infty} f(x)=L$$
	- if the following is true :
	- $$0 < |x-x_0| < \delta \quad \Rightarrow  |f(x)-L|< \epsilon$$
	- and so as $- \infty$
- oblique asymptotes
	- if $f(x)=g(x)/h(x)$ :
	- the remainder is the oblique asymptotes
	- where the other one is vertical 