---
title: Linear Algebra::Ch6
date: 2023-12-04 21:13:14
tags:
    - notes
    - linear algebra
---

## Inner product
- Axioms : 
    - Symmetry
    - Additivity
    - Homogeneity
    - Posotivity
- dot : Euclidean n-space
- All norm=1 : unit sphere
- Unusual unit circle : root both side

## Angle & orthogonality
- Obtain $\theta$ from arccos
- Cauchy-Schwarz inequality
- $d(\vec{u}, \vec{v}) \leq d(\vec{u}, \vec{w}) + d(\vec{w}, \vec{v})$
- Orthogol : inner product = 0
- W is subspace of V -> so is orthogonal complement

## Gram-Schmidt process & QR-Decomposition
- Orthonormal basis
- Projection theorem
    - $proj_{w}(\vec{u}) = (\vec{u} \cdot \vec{v_{1}})\vec{v_{1}} + (\vec{u} \cdot \vec{v_{2}})\vec{v_{2}}$
- Non-zero finite-dimensional innder product has orthonormal basis
- QR-decomposition : fatorize into :
    - Q : $m \times n$ orthogonal vectors 
    - R : $n \times n$ upper triangular matrix

## Best approximation & Least square
- Least squre problem : minimize $\| \vec{b} - A \vec{x}  \|$
    - $\| \vec{b} - A \vec{x}  \| = e_{1}^2 + ... + e_{m}^2$
    - The solution $A \hat{\vec{x}} = proj_{col(A)} \vec{b}$
    - $\| \vec{b} - proj_{w}\vec{b}  \| \leq \| \vec{b} - \vec{w} \|$
- Normal equation : $A^T A \vec{x} = A^T \vec{b}$
    - $(A^TA)^{-1}A^T \vec{b} = \vec{x}$
- Column vectors are linear independent : $A^TA$ is invertible
- QR : $\vec{x} = R^{-1}Q^{-1} \vec{b}$

## Mathematical modeling
- Least squares straight line fit : 
    - $M = \begin{bmatrix} 1 & x_{1} \\ ... & ... \\ 1 & x_{n} \end{bmatrix}$
    - $y = \begin{bmatrix} y_{1} \\ ... \\ y_{n} \end{bmatrix}$
    - $M^TM \vec{v} = M^T \vec{y}$
