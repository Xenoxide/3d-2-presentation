# Slide 1
Show the failed program

# Slide 2
I sometimes wonder how computers do things that we don't even think about. For example, compressing files to half their size, how they talk to each other over the internet, and how do they display 3D objects on a flat screen? The final one is my question. There is a lot of math involved.

# Slide 3
Let's say the pixels on the screen have the coordinates (x, y). Your object has points at the coordinates (x, y, z). Since you're going from 3 dimensions to 2 dimensions, couldn't you just remove the z component, the depth component? You can, this is an orthographic projection. All the lines are parallel, and things are the same size no matter how far away they are. The left picture is an orthographic projection.

# Slide 4
Artists may know another method. You draw 1, 2, or 3 vanishing points and draw objects on lines leading to those points. I'll revisit vanishing points later, but this is a perspective projection, and this is what I'm looking for. A perspective projection matches reality.

# Slide 5
A computer has a set of points and a screen of pixels. It doesn't know how to draw lines to vanishing points, because there's no sense of a sheet of paper. It only knows numbers. So it must have another strategy.

# Slide 6
Linear algebra. I'll just talk about what's relevant. When I'm referring to a matrix, I'm talking about the thing on the left. The thing on the right is a vector. Imagine it this way, you have a set of numbers, you use the matrix on them, and you get another set of numbers. Each of the numbers you get is a combination of the multiples of your initial numbers. This concept alone can carry the whole process of graphics. And AI. It also has a say in most, if not all forms of advanced science. There are many things you can do with vectors and matrices.

# Slide 7
You put the set of numbers through one matrix, and through another matrix, and another. Isn't there a better way to do this? You can combine two matrices to make another one, that does the same thing as both at the same time! This is called matrix multiplication. Careful though, the product of two matrices is different depending on the order that you do it! This is analogous to how applying two operations to something gives a different result, depending on the order.

# Slide 8
You may be familiar with 2 dimensional points. These have an X component and a Y component. To go to the point (2, 3), you travel 2 in the X direction and 3 in the Y direction. This concept can be extended to 3 dimensions. There is an X, Y, and Z component. For example, you may have the point (1, 2, 1). For the sake of calculation, a fourth point may be included, the W component, which is equal to 1. This is called homogeneous coordinates.

# Slide 9
How are 3D objects stored on the computer? There are a bunch of points, each with an X, Y, and Z component. These points are put together to form triangles, and these triangles alone form 3 dimensional shapes. The normal vector basically indicates which way the face is facing, and the vertex texture coordinates are like a map of how the texture should be stretched over the object. All 3D objects are made of triangles.

# Slide 10
Side note, throughout this process, the vanishing points exist, we just never use them.

# Slide 11
The model matrix is the matrix that moves the points to the place that you want them. This includes rotations and translations. 

# Slide 12
That is a two dimensional rotation matrix. How do you make it 3 dimensional? There's a trick. Rotate an object. Look at the poles of it. You'll notice that it looks just like a 2 dimensional rotation. We can do this in 3 directions, and we get 3 matrices. Notice the pattern? For the X rotation, the X row and column are ignored. For the y rotation, y row and column. Some intuition for this is that any point on the Earth's axis of rotation does not move. The North Pole does not go around the Earth.

# Slide 13
This is how you combine the matrices. This is one of the reasons that we are using 4x4 matrices instead of 3x3 matrices, because it allows you to put a translation in the matrix.

# Slide 14
The view matrix is the inverse matrix of the camera's model matrix. Inversion is a magic operation that gives you the opposite of a matrix. For example, if the camera is 2 to the left, the objects move 2 to the right. X times one divided by X is 1. Likewise, a matrix multiplied by its inverse is the identity matrix, which, like one, changes nothing when you multiply by it.

# Slide 15
When you look at something, your vision is shaped like a cone. For a rectangular camera, that's a rectangular pyramid. Cut near the vertex of the pyramid (called the near clipping plane), and at the end (far clipping plane). Hence, a frustum. Everything the camera sees is contained in this volume. The shape is determined by the shape of the screen, and the field of view. That's just what angle you can see.

# Slide 16
The projection matrix converts the objects in the viewing frustum to clip space. Clip space ranges from -1 to 1 in each direction. This works because objects get smaller and closer together as they get farther away, so far away objects are squished into the far wall of the clip space. The width and height are calculated with the FOV, and the aspect ratio. The near and far are the distances to the near and far clipping planes. Usually these are around 1 and 1000 respectively. 

# Slide 17
This is it. You multiply all the matrices together to move the point, and project it. Then you divide by w to adjust for scaling, and divide by z to get the final points. At this point, you have the X and Y values for the pixels.

# Slide 18
Don't forget, the order in which you apply them matters.

# Slide 19
You may ask, why are we using matrices and vectors? This is because having a single construct for every operation simplifies the process a lot. It also allows you to combine every step of the process with ease. This is why 3D projection is not a nightmare of equations, but just a few transformations.

# Slide 20

# Slide 21
I wrote my whole project in C. It's like a more primitive version of C++. Compared to more modern languages like JavaScript and Python, it gives you more power over the computer, but you need to be responsible with this power. The code here prints what the user inputs. If you type in something longer than 9 characters, it will crash. You have to be careful at this level of control. I like the language because of how low level it is, and how fast it is. It's a simple language.

# Slide 22
This shows the structure of the program I wrote. It starts with data about the camera and the object. The object is stored in an obj file, which I wrote a decoder for. This decoder converts the text into something the program can understand. Everything I discussed happens in the main routine. After the points are calculated, the output is sent to SDL to be printed to the screen. This utilizes Bresenham's line drawing algorithm. SDL also picks up input from the user to change the rotation of the camera. 

# Slide 23
I started by declaring a bunch of structs. Structs are like objects, but they don't have methods. This makes the data easier to work with, especially when dealing with pointers. 

# Slide 24
Then, I added the functions to decode OBJ files. It takes in the file, and returns a list of faces contained within the object. It also includes the normal vectors, but not the texture coordinates. I couldn't get far enough into the process to use the normal vectors. 

# Slide 25
Then, I added a bunch of arithmetic functions and functions to generate the matrices I talked about earlier. These work together to power the final function, which does the full transformation.

# Slide 26
I wrote a function to put the points in a face in the correct order. It's possible that they were received backwards. It checks for this by taking the cross product of two vectors within a triangle. A cross product finds a vector perpendicular to two vectors. The normal is the line perpendicular to the face, so this finds the normal. It then takes the dot product of that with the actual normal vector that comes with the shape. If it is negative, the vector is backwards, so the order of the points must be flipped.

# Slide 27
When writing code, it's a good idea to write unit tests to make sure your functions are working as intended. This is a test for a function that transposes the top left part of a matrix. This is used to invert the camera matrix. matrixcmp makes sure that the answer is correct. In my case, this function worked. I tested all the functions in my program, which helped me find mistakes and problems.

# Slide 28
This part of the code calls all the matrix generating functions for the first time, and reorders the points in the faces if necessary. These functions are called again when the values that they depend on are updated. For example, when the user scrolls, the FOV is increased or decreased, so the projection matrix must be updated. That's all I will show you.

# Slide 29
As I did this project, I learned a lot. I learned more about 3D rendering, and what mistakes I made the last time I did a project like this. I learned about text processing, which I've always struggled with. That is the fundamental component that makes programming languages work. I learned about unit tests and how to take command line input. I learned that it's a good idea to diagram your software. Importantly, I've overcome my fear of pointers, which are a crazy powerful concept in C. Overall, despite my program not working, this project was a success. Maybe I'll try again.

# Slide 30
To show your appreciation, make a wacky face.