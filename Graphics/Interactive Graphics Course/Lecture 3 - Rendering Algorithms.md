---
tags:
  - "#lecture"
links: https://www.youtube.com/watch?v=owx-R-Ary9I&list=PLplnkTzzqsZS3R5DjmCQsqupu43oS9CFN&index=4
---
# Rasterization
## Painter's Algorithm

paints objects based on distance to the camera, from back to front

**Drawbacks**:
- needs sorting
- cannot handle intersecting geometry

## Z-Buffer Rasterization

Stores the RGBA color value as well as the depth for each pixel, $\large z$.

Super Sample Anti-Aliasing (SSAA): storing multiple samples of RGBA and $\large z$ for each pixel; each pixel will have multiple color and depth values

Multi-Sample Anti-Aliasing (MSAA): storing a single sample of RGBA and multiple samples of $\large z$ for each pixel

**Pros/Cons**:
- can handle intersecting geometry
- needs sorting for transparency

## A-Buffer Rasterization

![[Pasted image 20240727102720.png|500]]

- can handle intersecting geometry
- supports order-independent transparency
- requires more dynamic memory

## REYES
**R**enders **E**verything **Y**ou **E**ver **S**aw

- splits shapes into micropolygons
# Ray Tracing
