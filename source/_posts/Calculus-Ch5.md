---
title: Calculus::Ch5
date: 2023-11-15 11:51:01
tags:
    - calculus
    - notes
---

## Estimate Area
Split into sub-interval using:
- Upper sum
- Lower sum
- Midpoint rule
## Finite sum limit
- Sigma notation
    - $\sum k = \frac{n(n+1)}{2}$
    - $\sum k^2 = \frac{n(n+1)(2n+1)}{6}$
    - $\sum k^3 = (\sum k)^2$
    - $\sum (\sum k) = \frac{n(n+1)(n+2)}{6}$
- Riemann sums
For closed interval [a, b] : 
$$
S_n = f(a + k \frac{b-a}{n}) \cdot (\frac{b-a}{n})
$$
## Definite integral
- Definition
    - Given $J$ the Riemann sum, $\epsilon > 0, \exists \delta > 0$, every partition P of [a, b] with $\|P\| < \delta$ : 
    - $\sum f(c_k) \Delta x_k - J < \epsilon$, 
$$
\lim \sum_{k=1}^{n} f(c_k) \Delta x = J = \int_a^b f(x)dx
$$
- Integrable
    - Continuous over [a, b] or finite jumps.
- Properties
    - Max-min inequality : $min \cdot (b-a) \leq J \leq max \cdot (b-a)$
    - Domination

## Fundamental theorem
- Mean value theorem
$$
f(c) = \frac{1}{b-a} \int_a^b f(x)dx
$$
- Fundamental theorem 
$$
F(x) = \int_a^x f(t)dt \\
F^{\prime}(x) = \frac{d}{dx}\int_a^x f(t)dt = f(x) \\
\int_a^b f(x)dx = F(b) - F(a) = \int_a^b F^{\prime} dx
$$
 
## Indefinite integral
- Indefinite
$$
\int f(x)dx = F(x)+C
$$
- Backward chain rule
$$
\int u^n \frac{du}{dx}dx = \frac{u^{n+1}}{n+1}+C
$$
- Backward chain rule substitute
If $u=g(x)$
$$
\int f(g(x))g^{\prime}(x) dx = \int f(u)du
$$
## Substitution
- In definite integral
If $g(x)=u$
$$
\int_{a}^b f(g(x)) \cdot g^{\prime}(x) = \int_{g(a)}^g(b) f(u)du
$$
- Symmetric functions
    - Even : $\int_{-a}^a f(x)dx = 2\int_{0}^a f(x)dx$
    - Odd : 0
- Area between curve
$$
A = \int_{a}^b (f(x) - g(x)) dx
$$
