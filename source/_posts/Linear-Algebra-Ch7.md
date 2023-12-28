---
title: Linear Algebra::Ch7
date: 2023-12-22 16:35:51
tags:
    - notes
    - linear algebra
---

## Orthogonal matrices
- Definition
    - $A^{-1} = A^{T}$
    - $AA^{T} = A^{T}A = I$
- Theorem
    - Row vectors & column vectors are orthogonal to each other
    - Inverse is orthogonal
    - Products are orthogonal
    - $det(A)=1$ or $det(A)=-1$
- Rotation in $R^3$
    - $P^{-1} = \begin{bmatrix} \cos \theta & \sin \theta & 0 \\ -\sin \theta & \cos \theta & 0 \\ 0 & 0 & 1 \end{bmatrix}$
## Orthogonal diagonalization
- Orthogonally similar : $B = P^{T}AP$
- Theorem
    - Eigenvectors are orthogonal
    - $A^T=A$
- Spectral decomposition
    - $P = [ \vec{u_{1}} \quad \vec{u_{2}} \quad ... \quad \vec{u_{n}} ]$
    - $A = PDP^T = \lambda_{1}\vec{u_{1}}\vec{u_{1}}^T + ... + \lambda_{n}\vec{u_{n}}\vec{u_{n}}^T$
- Nondiagonalizable case
    - Schur's theorem : with real entries and real eigenvalues, can find $P^TAP$ of the form : 
        - ![img](1.png)
        - Denote the upper matrix by S : $A=PSP^T$ (Schur decomposition)
    - Hessenberg's theorem : real entries, real eigenvalues, can find $P^TAP$ of the form :
        - ![img](2.png)
        - Denote the upper matrix by H : $A=PHP^T$ (upper Hessenberg decomposition)
## Quadratic forms
- Definition : $a_{1}x_{1}^{2} + ... + a_{n}x_{n}^{2}$
- Cross product term : $a_{k}x_{i}x_{j}$ where $i \neq j$
- Quadratic form associated with A : $Q_{A}(\vec{x}) = \vec{x}^TA\vec{x}$
    - In Geometry : Conic (circle, ellipse, parabola, hyperbola)
- Pricipal Axes Theorem : $\vec{x}^TA\vec{x} = \vec{y}^TD\vec{y} = \lambda_{1}y_{1}^2 + ... + \lambda_{n}y_{n}^2$
## Optimization
- Constrained extremum theorem
    - $\vec{x}^TA\vec{x}$ has max (eigenvector corresponds to) $\lambda_{1}$, min $\lambda{n}$, where $\|x\|=1$
    - $\|x\|=1$ : constraint
    - Level curves : $f(x, y)=k$ , in $R^2$ : $\vec{x}^TA\vec{x}=k$
    - Level curves touches at points $(x, y)$ at unit circle
    - Relative extrema : second derivative test
        - Hessian matrix : $det(H) = f_{xx}(x_{0}, y_{0})f_{yy}(x_{0}, y_{0})-f_{xy}^{2}(x_{0}, y_{0})$
        - Positive definite : $f$ has relative minimum
## Hermitian, Unitary, Normal matrices
- Conjugate transpose : $A^{*} = \bar{A^T}$
- Unitary matrix : $AA^* = A^*A = I$ or it's conjugate equals to inverse
    - Has orthogonal row vectors
- Hermitian matrix : $A^*=A$ : diagonal entries must be real
    - Has orthogonal eigenvectors
    - Unitarily diagonalize : Gram-Schmidt the eigenspace, then find P to diagonalize
