---
title: Linear Algebra::Ch5
date: 2023-11-28 13:46:19
tags:
    - notes
    - linear algebra
---

## Eigenvalue & eigenvector
- Eigenvalue : solve for characteristic equation
$$
det(A-\lambda I)=0
$$
- Eigenvector : solve for
$$
A \vec{x} = \lambda \vec{x}
$$

## Diagonalization
Solve for $\lambda$ , then
$$
P^{-1}AP
$$

## Complex vector spaces
- Complex eigenvalue
- Vectors in $C^n$
- Real & Imaginary
    - $\vec{v} = Re(\vec{v}) + i \cdot Im(\vec{v})$
    - Complex conjugate : $Re(\vec{v}) - i \cdot Im(\vec{v})$
- Inner product
    - Has same properties with $R^n$
    - Anitisymmetry
- Eigenvalue, eigenvector and conjugate
- $R^2$ eigenvalues based on discriminant:
    - $b^2-4ac>0$ : Two distinct real roots
    - $b^2-4ac=0$ : One root
    - $b^2-4ac<0$ : Two conjudate imaginary roots
- Real symmetric matrix : must have real eigenvalue
- Geometric interpretation : factorize into $cos, \quad sin$

## Differential equations
- First-order linear system
    - Solve by diagonalization
## Dynamical system & Markov chain
- State matrix
- Probability vector for state 1...n
    - Sum of probability = 1
- Stabilize
- Regular Markov chain : all entries positive
