---
tags:
  - research
links: https://www.youtube.com/watch?v=gQiD2Kd6xoE&list=PLplnkTzzqsZS3R5DjmCQsqupu43oS9CFN&index=2
---
# Notations

**Alpha** ($\large \alpha$): opacity
- $\large \alpha = 0$ means fully transparent
- $\large \alpha = 1$ means fully opaque

**Matrices**: 
$$\large
\begin{flalign}
\mathbf{A} =
\begin{bmatrix}
a_{00} & a_{01} & a_{02} \\

a_{10} & a_{11} & a_{12} \\ 

a_{20} & a_{21} & a_{22} \\
\end{bmatrix} &&
\end{flalign}
$$
# Affine Transformations
## Scale

Non-uniform scale:
![[Pasted image 20240726205038.png|300]]
$$\large
\begin{flalign}
\begin{bmatrix} 
p'_x \\
p'_y
\end{bmatrix}
=
\begin{bmatrix}
s_x \quad 0 \\
0 \quad s_y \\
\end{bmatrix}
\begin{bmatrix}
p_x \\ 
p_y
\end{bmatrix}
=
\begin{bmatrix}
s_x p_x \\
s_y p_y
\end{bmatrix} &&
\end{flalign}
$$
## Rotation

![[Pasted image 20240726205550.png|300]]
$$
\large
\begin{flalign}
\begin{bmatrix} 
p'_x \\
p'_y
\end{bmatrix}
= p_x
\begin{bmatrix}
\cos{\theta} \\
\sin{\theta} \\
\end{bmatrix}
+ p_y
\begin{bmatrix}
-\sin{\theta} \\
\cos{\theta} \\
\end{bmatrix}&&
\end{flalign}
$$
$$\large
\begin{flalign}
\begin{bmatrix} 
p'_x \\
p'_y
\end{bmatrix}
=
\begin{bmatrix}
\cos{\theta} \quad -\sin{\theta} \\
\sin{\theta} \quad \cos{\theta} \\
\end{bmatrix}
\begin{bmatrix}
p_x \\ 
p_y
\end{bmatrix}&&
\end{flalign}$$

## Some Matrix Properties

Any matrix can be decomposed (by singular value decomposition (SVD)) into:
$$\large
\mathbf{M} = \mathbf{US}\mathbf{V}^T
$$
\*where $\mathbf{U}$ is an orthogonal (rotation), $\large \mathbf{S}$ is a diagonal (scale), and $\large \mathbf{V}^T$ is an orthogonal (rotation)

Any series of rotations and scalings:
$$\large 
\mathbf{p'} = \mathbf{R}\mathbf{S}\mathbf{R}\dots\mathbf{S}\mathbf{R}\mathbf{p}
$$
can be condensed into the form:
$$\large \mathbf{p'} = \mathbf{M}\mathbf{p}$$
## Translation

We ideally want to keep our operations homogeneous instead mixing addition and multiplication. We want to change this:
$$\large \mathbf{p}' = \mathbf{p} + \mathbf{t}$$
into this:
$$\large \mathbf{p}' = \mathbf{T}\mathbf{p}$$
We can achieve this by using homogenous coordinates, which adds a component $1$ to effectively achieves addition while still using matrix multiplication.
$$\large
\begin{aligned}
& {\left[\begin{array}{c}
p_x^{\prime} \\
p_y^{\prime}
\end{array}\right]=\left[\begin{array}{l}
p_x+t_x \\
p_y+t_y
\end{array}\right]} \\
\end{aligned}
$$
$$\large
\begin{aligned}
& {\left[\begin{array}{c}
p_x^{\prime} \\
p_y^{\prime} \\
1
\end{array}\right]=\left[\begin{array}{lll}
1 & 0 & t_x \\
0 & 1 & t_y \\
0 & 0 & 1
\end{array}\right]\left[\begin{array}{c}
p_x \\
p_y \\
1
\end{array}\right]}
\end{aligned}
$$

# Transformations in 3D

## Scale
$$\large
\begin{bmatrix}
p'_x \\
p'_y \\
p'_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
s_x & 0 & 0 & 0 \\
0 & s_y & 0 & 0 \\ 
0 & 0 & s_z & 0 \\
0 & 0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix}
p_x \\
p_y \\
p_z \\
1
\end{bmatrix}
$$
## Translation
$$
\large
\begin{bmatrix}
p'_x \\
p'_y \\
p'_z \\
1
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & t_x \\
0 & 1 & 0 & t_y \\
0 & 0 & 1 & t_z \\
0 & 0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix}
p_x \\
p_y \\
p_z \\
1
\end{bmatrix}
$$
## Rotation

Represent rotation about any axis as a combination of rotations about x, y, and z axes.
$$ \large
\begin{array}{r}
\mathbf{R}_{\mathbf{x}}:\left[\begin{array}{cccc}
1 & 0 & 0 & 0 \\
0 & \cos \theta & \sin \theta & 0 \\
0 & -\sin \theta & \cos \theta & 0 \\
0 & 0 & 0 & 1
\end{array}\right] \\\\
\mathbf{R}_{\mathbf{y}}:\left[\begin{array}{cccc}
\cos \theta & 0 & -\sin \theta & 0 \\
0 & 1 & 0 & 0 \\
\sin \theta & 0 & \cos \theta & 0 \\
0 & 0 & 0 & 1
\end{array}\right] \\\\
\mathbf{R}_{\mathbf{z}}:\left[\begin{array}{cccc}
\cos \theta & \sin \theta & 0 & 0 \\
-\sin \theta & \cos \theta & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{array}\right]
\end{array}
$$
$$\large
\mathbf{p'} = \mathbf{R_z}(\alpha)\ \mathbf{R_z}(\beta)\ \mathbf{R_z}(\gamma)\mathbf{p}
$$
# Viewing

**View/Camera Space**: the camera space; coordinate system where the camera is positioned at the origin, aimed down the negative z-axis

**Model/Object Space**: each object has its own coordinate system so transformations can be applied. Each object has its own object space

**Scene/World Space**: the scene itself in which all the objects live

The model scenes and their respective model spaces are then transformed into the scene. These are all affine transformations, and there will be a single transformation matrix. 

# Projection
**Canonical View Volume**: part of the scene that is visible

![[Pasted image 20240726230514.png|350]]

Finally, the view/camera space will be transformed to the canonical view volume.

## Orthographic Projection

We use **orthographic projection** to achieve this. Orthographic projection matrix:
$$\large
\left[\begin{array}{c}
x^{\prime} \\
y^{\prime} \\
z^{\prime} \\
1
\end{array}\right]=\left[\begin{array}{cccc}
\frac{2}{r-l} & 0 & 0 & \frac{-2 l}{r-l}-1 \\
0 & \frac{2}{t-b} & 0 & \frac{-2 b}{t-b}-1 \\
0 & 0 & \frac{2}{f-n} & \frac{-2 n}{f-n}-1 \\
0 & 0 & 0 & 1
\end{array}\right]\left[\begin{array}{c}
x \\
y \\
z \\
1
\end{array}\right]
$$
## Perspective Projection

This is what you're already used to where there is an image plane.

![[Pasted image 20240726231559.png|350]]

This will be transformed into the canonical volume

![[Pasted image 20240726231813.png]]

This is done in two steps:
1. Perspective Transformation
2. Orthographic Projection

### Perspective Transformation
The transformation applied to make this happen:
![[Pasted image 20240726232338.png]]

**In more detail:**
![[Pasted image 20240726232922.png]]
- align at $\large n$, end at $\large f$
- for all points along the red line, $\large \frac{p_y}{p_z}$ is constant
$$\large
\large p'_x = \frac{p_x}{p_z}n
$$
$$\large p'_y = \frac{p_y}{p_z}n$$

[]
$$\large
\large
\left[\begin{array}{c}
x^{\prime} \\
y^{\prime} \\
z^{\prime} \\
1
\end{array}\right]=\left[\begin{array}{cccc}
n & 0 & 0 & 0 \\
0 & n & 0 & 0 \\
0 & 0 & ? & ? \\
0 & 0 & 1 & 0
\end{array}\right]\left[\begin{array}{c}
p_x \\
p_y \\
p_z \\
1
\end{array}\right]
$$
What about the transformation applied to $\large p_z$? Whatever transformation we apply to $\large p_z$ should preserve the original values as much as possible:
$$
\large
\left[\begin{array}{c}
x^{\prime} \\
y^{\prime} \\
z^{\prime} \\
1
\end{array}\right]=\left[\begin{array}{cccc}
n & 0 & 0 & 0 \\
0 & n & 0 & 0 \\
0 & 0 & n+f & -fn \\
0 & 0 & 1 & 0
\end{array}\right]\left[\begin{array}{c}
p_x \\
p_y \\
p_z \\
1
\end{array}\right]
$$
We can see that this works:
We want $\large p'_z = n$ when $\large p_z = n$:
$$\large
\begin{aligned}
p'_z &= ((n+f)p_z - fn) / p_z \\
&= (n+f) - fn / p_z \\
&= (n+f) - f \\
&= n
\end{aligned}
$$
And we need $\large p'_z = f$ when $\large p_z = f$
$$\large 
\begin{flalign}
p'_z &= (n+f) - n \\ 
&= f
\end{flalign}
$$
These are both true, so this is an appropriate transformation matrix.

## Whole Process

![[Pasted image 20240726235020.png]]