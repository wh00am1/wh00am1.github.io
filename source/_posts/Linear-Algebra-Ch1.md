---
title: Linear Algebra::Ch1
date: 2023-10-18 17:36:11
tags: 
	- linear algebra
	- notes
---

## Linear-equations
<!-- more -->
- $a_1x_1 + a_2x_2 + ... + a_nx_n = b$
- variables only have first power and wont involve below functions :
    1. trigonometric.
    2. logarithmic.
    3. exponential.

## Linear-system
### Definition

- A **finite set** of linear equations.
- solutions satisfies the system.
- solution exists = system **consistent**.

### Solutions

3 situations :

- no solution.
- exact one.
- infinite.

### Ways to find solution

- Gaussian Elimination :
    1. make every leading number 1 after the elimination can obtain **Row Echelon** (階梯型矩陣).
    2. if every leading 1 is the only non-zero in the row, it is the **Reduced Row Echelon Form.**
- back substitution
    - solve the leading unknowns first.
### Homogeneous Linear Systems(齊性)
#### fundamental characteristics
- every **constant element** in the system is 0.
- the solution is :
    1. $x_1 = x_2 = ... = x_n = 0$ as **trivial** ones.
    2. a line as **non-trivial** ones.

### Theorems
1. If there's $n$ variables, and the **reduced row echelon form** of its augmented matrix has $m$ non-zero rows, there are $n-m$ free variables in the system.
2. when unknowns are more than equations, the system has infinite solutions.
### Computer solution of Linear System
- reduce round-off errors (捨入誤差)
- optimize in both time and space complexity
## Matrix
### Definition
- A rectangular array of numbers.
- numbers = **entries.**
- **Equal matrices** : same size, same corresponding entries.
### Matrix transpose
- swap every $row$ with every $column$
- if $A=A^T$ → A is symmetric matrix
### Trace
- only defined if it’s a square matrix
- for a matrix $n \times n$, $tr(M) = M_{11} + M_{22} + .. + M_{nn}$
### Adjacent Matrix method to find inverse
- $A^{-1} = \frac{adj(A)}{det(A)}$
### Adjacent Matrix
- For every entry in the adjacent matrix(or adj(A)):
    - $adj(A)_{ji}=det(C_{ij})=det((-1)^{i+j}(M_{ij}))$
    - where $M_{ij}$ states for the origin matrix without the $i$’th row and the $j$’th column
- so theres a fast method for case $size(M)=2$ , that:
    - $M^{-1} = (\frac{1}{det(M)})(\begin{bmatrix} d & -b \\ -c & a \end{bmatrix})$