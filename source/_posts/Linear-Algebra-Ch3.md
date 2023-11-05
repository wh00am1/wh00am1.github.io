---
title: Linear Algebra::Ch3
date: 2023-10-18 23:22:49
tags:
	- linear algebra
	- notes
---

## Vectors in space
<!-- more -->
### Parallel and Collinear
- The vector $\vec{0}$ is regarded as parallel to all vectors
### Initial points
$$
\vec{P_1P_2} = (x_2-x_1, y_2-y_1)
$$
### n-Space
- $R^n=(v_1, v_2, ..., v_n)$ (ordered n-tuple)
#### Arithmetic
- Basic arithmetic
- $(k+m)u = ku+mu$
- $1u=u$
#### Linear combination
## Norm, Dot, Distance
### Norm
#### Basics
$$
\| \vec{v} \| = \sqrt{(v_1)^2+(v_2)^2+...+(v_n)^2}
$$
#### Normalize
$$
u = \frac{1}{\| \vec{v} \|} v
$$
### Dot
#### In 2D and 3D
$$ 
\vec{u} \cdot \vec{v} = \| \vec{u} \| \| \vec{v} \| cos \theta = \frac{1}{2}(\| \vec{u} \|^2+\| \vec{v} \|^2-\| \vec{u} - \vec{v} \|^2)
$$
#### In $R^n$
$$
\vec{u} \cdot \vec{v} = u_1v_1 + u_2v_2 + ... + u_nv_n
$$
### Distance in $R^n$
$$
d(u, v) = \| u-v \| = \sqrt{\sum{(u_i-v_i)^2}}
$$
## Orthogonality(正交)
### Basics
- Dot = 0
### Line and Plane based on Point and Normal
- Normal :
$$
\vec{n} \cdot \vec{L} = 0
$$
- Can be written(normal : $n(a, b, c)$):
$$
a(x-x_0)+b(y-y_0)+c(z-z_0)=0
$$
### Orthogonality Projection
$$
proj_a u = \frac{u \cdot a}{\| \vec{a} \|^2} a
$$
### Distance of Line and Plane
$$
D = \frac{\| ax_0 + by_0 + c \|}{\sqrt{a^2 + b^2 + c^2}}
$$
## Geometry of linear system
### Parametric Equations
$$
x = x_0 + t \vec{v}
$$
### Dot product of Linear System
- A and x is orthogonal in homogeneous linear system
## Cross product
### Cross product of vectors
let $\vec{u}$ and $\vec{v}$ be in 3-space
$$
\vec{u} \times \vec{v} = (u_2v_3 - u_3v_2, u_3v_1-u_1v_3, u_1v_2 - u_2v_1)
$$
### Determinant form
### Geometric interpretation
$$
\| \vec{u} \times \vec{v} \|^2 = \| \vec{u} \|^2 \| \vec{v} \|^2 sin \theta
$$
### Triple Product
$$
\vec{u} \times \vec{v} \cdot \vec{w}
$$
- 四面體體積 = Triple product / 6
