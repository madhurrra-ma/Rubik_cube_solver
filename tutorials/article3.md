3D Array Representation
One of the most basic representations can be simply storing the colors of a face in a 3-dimensional array of size 6 × 3 × 3, which would look something like:

cube[SIDE][ROW][COL]
cube[i][j][k] → color of the ith side, jth row and kth column.

We can index the faces any way we'd like but we need to keep them uniform throughout the code.

One way to index them is:

Up → 0 (White)
Left → 1 (Green)
Front → 2 (Red)
Right → 3 (Blue)
Back → 4 (Orange)
Down → 5 (Yellow)
Task 2: 3D Array Representation
Write an implementation of the 3D Array Representation of a Rubik’s Cube as described above. Derive this class from the Generic Rubik’s Cube class that we created in Task 1. Implement the necessary operations (all the virtual functions in the Generic Cube).

Reference Link for Task 2
RubiksCube3dArray.cpp