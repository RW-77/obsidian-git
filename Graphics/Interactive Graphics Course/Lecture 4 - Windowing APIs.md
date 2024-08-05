# Windowing APIs
- Open OS window
- Initialize OpenGL canvas
- Capture input devices
	- keyboard
	- mouse

## Windowing APIs for Open GL
- GLUT
- FreeGLUT (updated GLUT)
- GLFW
- Qt

# Glut

```
#include <GL/glut.h>
```

**Structure**:
```cpp
int main(int argc, char** argv)
{
	// GLUT Initializations
	...
	
	// OpenGL Initializations
	...
	
	// Other Initializations
	...
	
	glutMainLoop(); // Call main loop
	
	return 0; // Exit when main loop is done
}
```

## GLUT Initializations

```cpp
// Initialize GLUT
glutInit(&argc, argv);

// Create a window
glutInitWindowSize(1920, 1080);
glutInitWindowPosition(100, 100);
glutInitDisplayMode(
	GLUT_DOUBLE|GLUT_RGBA|GLUT_DEPTH );
glutCreateWindow("Window Title");

glutDisplayFunc(myDisplay);
glutKeyboardFunc(myKeyboard);
glutIdleFunc(myIdle);
...
// OpenGL Initializations
...
```

Tell GLUT which function will be your drawing function:
```cpp
// Register display callback function
glutDisplayFunc(myDisplay);

void myDisplay()
{
	// OpenGL draw calls here
}
```

```cpp
// Register keyboard callback function
glutKeyboardFunc(myKeyboard);

void myKeyboard(
	unsigned char key,
	int x, int y )
{
	// Handle keyboard input here
}
```

```cpp
// Register mouse callback function
glutMouseFunc(myMouse);

void myMouse(
	int button, int state,
	int x, int y )
{
	// Handle mouse buttons here
}	
```

```cpp
// Register mouse motion callback
glutMotionFunc(myMouseMotion);

void myMouseMotion(
	int x, int y )
{
	// Handle mouse motion here while a button is down
}
```

```cpp
glutPassiveMotionFunc(myMousePassive);

void myMousePassive(
	int x, int y )
{
	// Handle mouse motion here while a button is NOT down
}
```

```cpp
// Register window reshape callback
glutReshapeFunc(myReshape);

void myReshape(
	int x, int y )
{
	// Do what you want when window size changes
}
```

```cpp
// Register idle callback function
glutIdleFunc(myIdle);

void myIdle()
{
	// Handle animations here
}
```

# OpenGL Initializations

```cpp
// Set the background color
glClearColor(0, 0, 0, 0);

// Create buffers
// Create textures
// Compile shaders
```

# Display Function
- sometimes OpenGL should be the one calling this function
- other times, you will need to manually call this function
```cpp
void myDisplay()
{
	// Clear the viewport
	glClear( GL_COLOR_BUFFER_BIT 
		| GL_DEPTH_BUFFER_BIT );
	
	// OpenGL draw calls here
	
	// Swap buffers
	glutSwapBuffers();
}
```

# Double Buffering

**Front Buffer**: what the user sees
**Back Buffer**: what we are currently drawing

Once the drawing is complete, we will swap the buffers. This way, the user always sees a complete render.

![[Pasted image 20240727131756.png|400]]

We have to tell GLUT that we want double buffers:
```cpp
glutInitDisplayMode( GLUT_DOUBLE|GLUE_RGBA|GLUT_DEPTH );
```

# Idle Function

```cpp
void myIdle()
{
	// Handle animations here
	// Example:
	glClearColor(red, 0, 0, 0);
	red += 0.02;
	
	// Tell Glut to redraw
	glutPostRedisplay();
}
```

# Keyboard Function

```cpp
void myKeyboard(
	unsigned char key,
	int x, int y )
{
	switch ( key ) {
		case 'a':
			// Do something
			break;
	}
	// re-render
	glutPostRedisplay();
}
```

# GLFW

```cpp
#include <GLFW/glfw3.h>

int main(void)
{
	// Initialize the library
	if (glfwInit()) return -1;
	
	// Create a window
	GLFWwindow *window = glfwCreateWindow(
		640, 480, "Title", NULL, NULL);
	if ( !window ) {
		glfwTerminate ();
		return -1;
	}
	
	// Make the window's context current
	g]fwMakeContextCurrent(window);
	
	// Loop until the user closes the window
	while (glfwWindowShouldClose(window))
	{	
		gIClear (GL_COLOR_BUFFER_
		
		_BIT) ;
		
		// OpenGL calls here
		
		glfwSwapBuffers(window);
		
		// Poll for and process events
		
		glfwPollEvents();
	}	
	glfwTerminate();
	return 0;
}
```