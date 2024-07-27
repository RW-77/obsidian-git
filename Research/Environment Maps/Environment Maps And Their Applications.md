---
tags:
  - research
links: https://userpages.cs.umbc.edu/olano/s2000c27/envmap.pdf
---
# Introduction

**Primary uses of environment maps:**
- simulate reflections in curved objects
- store precomputed directional information that is too expensive to compute on the fly

**Fundamental Assumption:**
If an object is small relative to its distance from the environment, illumination on the surface (at the center of the environment) depends really only on direction of reflected ray.

*Think about it like this*: to render an object, we would usually have to shoot rays towards all points on its surface and see where those rays end up, in which case the reflection rays all have different origins. In classical raytracing, the exact origins are important because you need the precise parametrization of the resulting reflection ray for accurate objection collision detection and subsequent coloring. If you ignore these differences, a ray that originally would have hit the very edge of an object might now hit nothing.

But for an environment map that is very large relative to the object (in which the background "objects" do not need to be modeled directly), those small differences in the origins of the reflection rays don't mean much anymore. A change in the origin of the reflection ray can only be as large as the maximum distance between any two points on the object surface, which in comparison to the environment map, means very little. For a given ray $\large \alpha(t) = \mathbf{a} + \mathbf{v}t$, a small change to the ray origin, $\large \delta{\mathbf{a}}$, offsets the collision point $\large \alpha(t_{e})$ by approximately same amount so that it becomes $\large \alpha(t_{e}) + \delta{\mathbf{a}}$.

Therefore, we can treat every vector as originating from the center of the object which we define.
# Parameterizations for Environment Maps

Environment maps represent directional information as 2D texture, meaning there must be a way to map directions to texture coordinates. This is called a *parameterization*.

- Method for computing texture coordinates should be: simple, efficient, easy to implement in hardware
- For walkthroughs of static environments, it should not be necessary to create a new environment map every frame
- For interaction with dynamic environments, it should be easy and inexpensive to create a new environment map from perspective images of the scene

## Spherical Maps

Imageine small, fully specular metal ball centered around the object. The image an orthographic camera sees is on the metal ball.
