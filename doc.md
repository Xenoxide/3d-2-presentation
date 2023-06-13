---
title: "Computer Graphics: How does the computer make 3D objects 2D?"
author: "Aseer Tayeem"
linkstyle: bold
topic: "Linear algebra of 3D projection"
aspectratio: 169
header-includes:
  - \usepackage{gensymb}
  - \usetheme{metropolis}

---
# Question <!-- Slide 2 -->
![](images/1_huffman_coding.png){height=100} \ ![](images/2_lorenz_cipher.jpg){height=100} \ ![](images/3_utah_teapot.png){height=100}

# Trivial solution <!-- Slide 3 -->
If you have some 3D points with the coordinates $(x, y, z)$, you may be tempted to project them onto the screen at the coordinates $(x, y)$. This is called an orthographic projection. See (a).
![](images/4_projections.jpg){height=180}

# Perspective drawing <!-- Slide 4 -->
![](images/5_vanishing_points.jpg){height=200}

# What does the computer know? <!-- Slide 5 -->
The computer knows nothing but numbers. The computer doesn't know what a shape is, what geometry is. We need to turn our shapes into numbers, give it to the computer, and turn the numbers back into shapes.

![](images/6_bresenham.gif){height=125} \ ![](images/7_line.svg){height=125}

# Linear algebra <!-- Slide 6 -->
Equations:
$2x - 3y = 4$
$3x - 5y = -1$

Matrix and vectors:
$
\begin{bmatrix}2 & -3 \\ 3 & -5\end{bmatrix}
\begin{bmatrix}x \\ y\end{bmatrix}= 
\begin{bmatrix}4 \\ -1\end{bmatrix}
$

# Matrix multiplication <!-- Slide 7 -->
Improvements like these are called *optimizations*. \
![](images/8_inefficient_multiplication.png){height=125} \ ![](images/9_better_multiplication.png){height=125}

Add one then square it: $(x + 1)^2$
Square it then add one: $x^2 + 1$

# Points in 3 dimensions <!-- Slide 8 -->
![](images/10_2d_cartesian_coordinates.png){height=125} \ ![](images/11_3d_cartesian_coordinates.png){height=125}

# 3D objects <!-- Slide 9 -->
