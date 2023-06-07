# Slide 2
I sometimes wonder how computers do things that we don't even think about. For example, compressing files to half their size, how they talk to each other over the internet, and how do they display 3D objects on a flat screen? The final one is my question. There is a lot of math involved.

# Slide 3
Let's say the pixels on the screen have the coordinates (x, y). Your object has points at the coordinates (x, y, z). Since you're going from 3 dimensions to 2 dimensions, couldn't you just remove the z component, the depth component? You can, this is an orthographic projection. All the lines are parallel, and things are the same size no matter how far away they are. The left picture is an orthographic projection.

# Slide 4
Artists may know another method. You draw 1, 2, or 3 vanishing points and draw objects on lines leading to those points. I'll revisit vanishing points later, but this is a perspective projection, and this is what I'm looking for. A perspective projection matches reality.

# Slide 5
A computer has a set of points and a screen of pixels. It doesn't know how to draw lines to vanishing points, because there's no sense of a sheet of paper. It only knows numbers. So must have another strategy.