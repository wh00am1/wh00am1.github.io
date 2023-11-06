---
title: Calculus::Ch4
date: 2023-11-05 18:29:10
tags:
    - calculus
    - notes
---

## Extreme values
### Absolute extreme value
- Global maxima $f(c)$ in domain $D$ if:
$$
\forall x \in D, \quad f(x) \leqslant \ f(c)
$$
- Extreme value theorem
    - Given $f$ continuous in `[a, b]`, exists global maximum and minimum in `[a, b]`
### Local extreme value
- Relative minimum $f(c)$ in domain $D$ if in an open interval:
$$
\forall x \in D, \quad f(x) \geqslant \ f(c)
$$
- First derivative theorem (critical point)
$$
f^{\prime}(c) \quad = \quad 0
$$
## Mean value theorem
### Rolle's theorem
- Suppose $y=f(x)$ continuous at `[a, b]`, differentiable at `(a, b)`, $a \leqslant b \leqslant c$ if:
$$
f(a) \quad = \quad f(b)
$$
Then
$$
f^{\prime} (c)  = 0
$$
### Mean value theorem
- Suppose $y=f(x)$ continuous at `[a, b]`, differentiable at `(a, b)`, then $a \leqslant b \leqslant c$ where:
$$
\frac{f(b) - f(a)}{b - a} \quad = \quad f^{\prime}(c)
$$
## First derivative test(for local extreme value)
- Detect if $f^{\prime}$ changed between positive and negative
- Sign not changed -> no local extrema
## Concavity & sketching
### Concavity
- Quick solve
$$
\frac{d^2}{dx^2} f(x)
$$
- Point of inflection : $f^{"}(c) = 0$
- Second derivative test(for local extreme value)
    - Detect if $f^{"}(c)=0$
### Sketching procedure
1. Define domain
2. Derivative (both)
3. Critical point
4. inc/dec, inflection, concavity
5. Asymptooes
## L'Hopital's rule
- Use when:
    1. Indeterminate form ($\frac{0}{0}$, $\frac{\infty}{\infty}$, ...)
    2. The limit exist, or is infinite (can't use when DNE)
- The rule itself
$$
\lim \frac{f(x)}{g(x)} \quad = \quad \lim \frac{f^{\prime}(x)}{g^{\prime}(x)}
$$
## Applied optimization
1. Define the function
2. Use $f^{\prime} (x)$ to find max/min
## Newton's method
- A first approximation is needed
$$
x_{n+1} \quad = \quad x_n - \frac{f(x_n)}{f^{\prime}(x_n)}
$$
- Obtain approximate value by iteration
## Antiderivative
- Function $f(x)$
- Antiderivative : $F(x) + C$
