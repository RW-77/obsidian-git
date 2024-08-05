# The Graphics Rendering Pipeline
![[Pasted image 20240804101905.png]]
- **Green Stages** are *programmable*
- **Orange Stages** are *configurable*
## Detailed Description of Pipeline

1. **Application Stage**: represents the C++ side of the process, prepares the environment for encoding GPU commands for rendering.
2. **Vertex Shader Stage**: responsible for processing vertex data, applying transformations, and passing the resulting data to the next stages of the rendering pipeline. Requires vertex descriptors when feeding vertex data to Metal Vertex Shader.
3. **Rasterization Stage**: converts vector-based geometry (vertices) into pixel-based fragments
4. **Fragment Shader Stage**: responsible for processing and shading pixel-based fragments generated during rasterization.
5. **Blending Stage**: responsible for combining the output of the Fragment Shader stage with the existing data in the framebuffer, considering factors like transparency, translucency, and depth. Determines the final color of each pixel by blending incoming fragment color with color already present in framebuffer.