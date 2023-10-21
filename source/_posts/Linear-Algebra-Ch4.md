---
title: Linear Algebra::Ch4
date: 2023-10-21 13:43:16
tags: 
	- linear algebra
	- notes
---

## Real Vector Spaces
<!--more-->
### Axioms
- 8 Axioms from $R^n$
- **Zero Vector** exists in $V$ that $0+u = u+0$ for all $u$ in $V$
- For each $u$ in $V$ exists $-u$
- The elimination method works
- $0u = 0$
## Subspaces
### Terminology
#### Definition
- Subset $W$ is under scalar manipulation defined in $V$ 
- Not inherited Axioms:
	- Closure of $W$ (under addition and multiplication)
	- Zero vector in $W$
	- Exist a negative one for all vector in $W$
### Testing subspaces
- $u+v$ in $W$
- $ku$ in $W$
### Building Subspaces
#### Creating from known Subspaces
- For subspace $W_1, W_2, ..., W_n$, the intersections are also subspace of $V$
#### Solution Spaces of Homogeneous
- $n$ unknowns : subspace of $R^n$
#### Linear transformation
- Kernel of transformation is a subspace of $R^n$
## Spanning Sets(生成空間)
### Definition
- Given subset $S={ \vec{v_1}, \vec{v_2}, ..., \vec{v_n} }$ from $V$:
$$
span(S) = span( \vec{v_1}, \vec{v_2}, ..., \vec{v_n} )
$$
- $span(S)$ can also be defined as a set of all Linear Combination formed by the element in $S$
- If Vector Space $V$ and Set $S$ are both infinite, the Linear Combinations are not guaranteed to be in $span(S)$
## Linear Independence
### Definition
- Given $V$ in Field $K$ ($ \vec{v_1}, \vec{v_2}, ..., \vec{v_n}$ and $a_1, a_2, ..., a_n$), if the following does not exits in $K$:
$$
a_1 \vec{v_1} + a_2 \vec{v_2} + ... + a_n \vec{v_n} = 0
$$
- If any Subset of infinite Set in $V$ is Linearly Independent, the original Set is Linearly Independent
### Properties
- The following Vector Sets are **Linearly Dependent**:
	- Contains $\vec{0}$
	- Contains two same vectors
	- A Linear Dependent Set with one more arbitrary vector
	- `sizeof(Set)>n`
- Dependent or not remains the same:
	- Part of Linear Independent
	- Adding component vector in every vector
- If `set1` with size `sz1` can be expressed in Linear Combination of `set2` with `sz2` where `sz1`>`sz2`, `set1` is
	Linearly Dependent
## Coordinates and Basis
### Coordinate system
- Non-perpendicular axes
### Basis
#### Definition
- $S$ is Basis for $V$ if:
	- $S$ spans $V$
	- $S$ is Linearly Independent
### Relative
- If $S\{v_j\}$ is Basis of $V\{v_i\}$:
	- $\vec{v_i} = \sum{c_j \vec{v_j}}$
	- Scalars $c$ are **coordinates of $v_i$ to ordered S**
## Dimension
### Fundamental theorems
- All bases for a Finite-Dimensional Vector Space have same number of vectors
- Given $V$, and any Basis of $V=\{v_1, v_2, ..., v_n\}$
	- If a Set in V `sizeof(Set)>n`, it's Linearly Dependent
	- If `sizeof(Set)<n`, it's not able to span $V$
- Dimension of $V$ ( or $dim(V)$ ) = $n$
	- $dim(R^n) = n$
	- $dim(P_n) = n+1$
	- $dim(M_{mn}) = mn$
	- $dim(span(v_1, v_2, ..., v_n)) = n$
	- Dimension of Solution Space is the least number of unknowns to express solution
### Other theorems
- Plus/Minus Theorem
Let $S$ be nonempty subset of $V$:
	- Inserting $\vec{v}$ that's not in $span(S)$ wont make become $S$ Linearly Dependent
	- $span(S) = span(S - \{v\}) if $\vec{v}$ can be expressed as Linear Combination in $S$
- Given $V$ is $n$-dimensional, and subset $S$ with size $n$:
	- $S$ is Basis for $V$ if :
		- $S$ spans $V$
		- $S$ is Linearly Independent
- Given $S$ be finite subset of finite-dimensional $V$:
	- If $S$ spans $V$ : $S$ can be reduced to a Basis for $V$
	- If $S$ if Linearly Independent set: $S$ can be enlarged to a basis for $V$
- Given $S$ a subspace of finite-dimensional vector space $V$:
	- $S$ is finite-dimensional
	- $dim(S) \leqq dim(V)$
	- $S=V$ if $dim(S) = dim(V)$
## Change of Basis
### Change-of-Basis Problem
#### 2D Spaces
1. Basis $B = \{\vec{u_1}, \vec{u_2}\}$ and $B' = \{\vec{u_1'}, \vec{u_2'}\}$
2. Suppose coordinate vectors relative to the new basis are:
$$
\vec{u_1}  = a \vec{u_1'} + b \vec{u_2'} \\
\vec{u_2} = c \vec{u_1'} + d \vec{u_2'}
$$
3. Suppose old coordinate for any vector $\vec{v}$ in $V$:
$$
[\vec{v}]_{B'} = [k_1 \vec{u_1}, \quad k_2 \vec{u_2}]
$$
4. Substitute the above statements amd get new coordinate vector
$$
\vec{v} = k_1(a u_1' + b  u_2') + k_2(c u_1' + d u_2')
$$
$$
[\vec{v}]_{B'} = [k_1a + k_2c, \quad k_1b + k_2 d]
$$
5. States taht the new coordinate vector is the old coordinate vector multiplied by:
$$
P = \begin{bmatrix} a & b \\ c & d \end{bmatrix}
$$
### Computs Transition Matrices for $R^n$
- [ new basis | old basis ] (use row operation)
- [ $I$ | transition from old to new]
### Transition to the Standard Basis
- Given $B = \{\vec{u_1}, \vec{u_2}, ..., \vec{u_n} \}$ be any Basis for $R^n$, $S$ be standard Basis for $R^n$, then:
$$
P_{B \to S} = [ \vec{u_1} | \vec{u_2} | ... | \vec{u_n} ]
$$
- Also if the following is invertible:
$$
A = [ \vec{u_1} | \vec{u_2} | ... | \vec{u_n} ]
$$
Then  A can be viewed as Transition Matrix to Standard Basis
## Row Space, Column Space and Null Space
### Definition
- In $m \times n$ matrix A:
	- Row vectors : in $R^n$ form
	- Column vectors : in $R^m$ form
	- $row(A)$ : subspace of $R^n$ spanned by row vectors
	- $col(A)$ : subspace of $R^n$ spanned by column vectors
	- Homogeneous $Ax=0$ sol' space : $null(A)$, the null space of $A$
- Linear Sytem $Ax=b$ is consistent if:
	- $b$ is in Column space of $A$
### $Ax=b$ and $Ax=0$
- 
## Rank, Nullity, Fundamental Matrix Spaces
