---
title: Linear Algebra::Ch2
date: 2023-10-18 22:51:45
tags:
	- linear algebra
	- notes
---

## Evaluate by Cofactor Expansion
<!-- more -->
### Expand the first row for example
$$ det(M) = m_{11}C_{11}+m_{12}C_{12}+...+m_{1n}C_{1n} $$
### Evauate 3x3 matrix quick method
$$ det(M) = m_{11}m_{22}m_{33}+m_{12}m_{23}m_{31}+m_{13}m_{21}m_{33}-m_{13}m_{22}m_{31}-m_{12}m_{21}m_{33}-m_{11}m_{23}m_{32} $$
## Evaluate by Row Reduction
### Determinant of Elementary Matrix
- Let $E$ be $n \times n$ Elementary Matrix
- If:
	1. Multiply a row by $k$, then $det(E)=k$
	2. Interchanging 2 rows, then $det(E)=-1$
	3. Adding a row(k times), then $det(E)=1$
### Evaluation
1. Reduce to row echelon
2. Evaluate by :
$$ det(M) = tr(M) $$
## Properties
With $n \times n$ matrix A, B :
1. $det(kA)=k^n det(A)$
2. $det(A)det(B)=det(AB)$
3. seperate entries of a row/column: $det(A_1)+det(A_2)$
## Cramer's Rule
### Basic
With $n \times n$ matrix A, $1 \times n$ matrix B and $Ax=B$ linear system:
1. The solution is:
$$ x_n = \frac{det(A_n)}{det(A)} $$
### Properties
1. Can use the method only when A is invertible.