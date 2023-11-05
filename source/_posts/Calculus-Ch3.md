---
title: Calculus::Ch3
date: 2023-11-05 18:29:06
tags:
    - calculus
    - notes
---

## Derivative at a point
provided that the limit exists:
$$
m \quad = \quad \lim_{h \to 0} \frac{f(x_0 + h) - f(x_0)}{h}
$$
## Derivative as a function
provided that the limit exists:
$$
f^{\prime}(x) \quad = \quad \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}
$$
or:
$$
f^{\prime}(x) \quad = \quad \lim_{a \to x} \frac{f(a) - f(x)}{a-x}
$$
## Differentiation rules
### Power rule
$$
\frac{d}{dx} x^n \quad = \quad n x^{(n-1)}
$$
### Product rule
$$
\frac{d}{dx} (uv) \quad = \quad u \frac{dv}{dx} + v \frac{du}{dx}
$$
### Quotient rule
$$
\frac{d}{dx} (\frac{u}{v}) \quad = \quad \frac{ v \frac{du}{dx} - u \frac{dv}{dx}}{v^2}
$$
### e rule
$$
\frac{d}{dx} (e^x) \quad = \quad e^x
$$
### Higher order
$$
\frac{d^2 y}{dx^2} \quad = \quad \frac{d}{dx} (\frac{dy}{dx}) = \frac{dy^{\prime}}{dx}
$$
## Rate of change
### Instantaneous rate of change
velocity (if exists):
$$
f^{\prime}(x_0)
$$
## Trigonometric functions
- $\frac{d}{dx} sin(x) \quad = \quad cos(x)$
- $\frac{d}{dx} cos(x) \quad = \quad -sin(x)$
- $\frac{d}{dx} tan(x) \quad = \quad sec^2(x)$
- $\frac{d}{dx} sec(x) \quad = \quad sec(x) tan(x)$
## Chain rule
$$
\frac{dy}{dx} \quad = \quad \frac{dy}{du} \cdot \frac{du}{dx}
$$
## Implicit differentiation
- Differentiate both side
- Collect $\frac{dy}{dx}$
## Inverse
### Inverse
$$
(f^{-1})^{\prime} (x) \quad = \quad \frac{1}{f^{\prime} (f^{-1}(x))}
$$
### Logarithm
$$
\frac{d}{dx} ln(x) \quad = \quad \frac{1}{x}
$$
### Trigonometric
$$
tan^{-1} (-x) \quad = \quad -tan^{-1} (x)
$$
- in some cases:
$$
sec^{-1} (x) \quad = \quad cos^{-1} (\frac{1}{x})
$$
- use implicit

$\frac{d}{dx} sin^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{\sqrt{1-u^2}}$

$\frac{d}{dx} cos^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{\sqrt{1-u^2}}$

$\frac{d}{dx} tan^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{1+u^2}$

$\frac{d}{dx} cot^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{1+u^2}$

$\frac{d}{dx} sec^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{|u|\sqrt{u^2-1}}$

$\frac{d}{dx} csc^{-1}(u) \quad = \quad \frac{du}{dx} \frac{1}{|u|\sqrt{u^2-1}}$
## Related rates
Combine numerical informations
## Linearization and differentials
### Linear approximation
when at x=a
$$
L(x) \quad = \quad f(a) + f^{\prime}(a)(x-a)
$$
### Independent ratio
$$
dy \quad = \quad f^{\prime}(x) dx
$$
