Vertices are transformed with transformation matrices to different spaces defined by separate coordinate systems. OpenGL and other graphics APIs expect vertices to be in normalized device coordinates within $\large [-1.0, 1.0]$. 
# Prerequisites & Terminology
## Spaces
- Local space / Object space
- World space
- View space / Eye space
- Clip space
- Screen space
## Transformations
- Model matrix
- View matrix
- Projection matrix
## The Global Picture

![[Pasted image 20240805165156.png|500]]
# Local Space
The coordinate space that is local to an object. For example, a cube could have a coordinate system defining one of its corners as $\large (0, 0, 0)$.

Why even have local spaces? Why not just objects directly in the world space as was done in ROTW? This has to do with portability, where objects are often modeled separately so they can be imported into any scene.
# World Space
If we were to import all our individual objects directly, they would all be somewhere near $\large (0, 0, 0)$ since they were modeled that way, and so they would all be inside of each other. Obviously, we need some new kind of coordinate system.

The coordinates in the world space define where your vertices are relative to some "world." The *model matrix* will translate, scale, and/or rotate objects to their appropriate positions in the world space.
# View Space
So we have a world space now. But that is not enough, the objects in the world space are going to be rendered from some viewpoint. The view space is thus the space as seen from the camera's point of view.

This is done through a combination of translations and rotations so that certain items are transformed to the front of the camera. These are stored inside a *view matrix* which transforms world coordinates to view space.
# Clip Space
But we aren't done yet. Not everything in the world is going to be rendered in a given frame. That's why we have the clip space. Anything outside this clip space will be clipped, so only coordinates that fall within will be run through the fragment shader.

We use a *projection matrix* which takes a range of coordinates e.g. $\large [-1000, 1000]$ in each dimension (so basically a $\large 2000$ x $\large 2000$ x $\large 2000$ box). All coordinates within this range are then converted to *normalized device coordinates* (NDC) which the graphics API expects e.g. $\large (-1.0, 1.0)$.

The projection matrix to transform view coordinates to clip coordinates can either be an *orthographic projection* matrix or a *perspective projection* matrix. The *viewing box* a projection matrix creates is a *frustum*, and all coordinates inside the frustum will end up on the screen.