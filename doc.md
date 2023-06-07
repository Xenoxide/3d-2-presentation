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
The computer only handles numbers. When it seems to do geometry, it has been tricked into doing it.

# Linear algebra <!-- Slide 6 -->
