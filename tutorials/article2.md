Rubik’s cube is a real-world object. The first part of our project would be to try to take this real-world Rubik's cube and model it in some form that our computer can understand. This model should include everything necessary to define the unique state of a Rubik’s Cube. Also, it should support different operations like rotations (F, U2, B’, etc), so that we can write programs to solve them. Theoretically, we can model it in any form but we would ideally want to model it in a way that is fast to do operations/rotations upon.

Generic Cube
Going further, we are going to discuss various ways to model a Rubik’s Cube. But all of those implementations are going to have some common features. They all are going to support some common operations. So, instead of keeping all of these implementations completely independent, we can create a layout/blueprint for them which will state all things that the Model should implement. If you know about Object-Oriented Programming, you would recognize creating layouts/blueprints is a common theme. In this case, we would like to create abstract classes and pure virtual functions representing the Generic Cube.


 

If you want to read more about abstract classes and pure virtual functions, you can read it from here: 

https://www.learncpp.com/cpp-tutorial/pure-virtual-functions-abstract-base-classes-and-interface-classes/

 

If you are not familiar with Object-Oriented Programming in C++, you can spend some time learning the basics from 

https://www.learncpp.com/ (Chapter 12, 13, 16, 17, and 18).


 

We are going to create an abstract class of Rubik’s Cube, which would have certain common operations as virtual functions. We would take this Base Class and create Derived Classes for each representation. That way we can ensure a uniform structure to all our representations. 

Before going further try to list down things that you think would be common in each implementation.

Task 1: Generic Rubik’s Cube:
Write an abstract class of a Generic Rubik’s Cube that has the following operations as virtual functions:

All the 18 different rotations of the cube: F, Fprime, F2, U, Uprime, etc.
Print function: A function that takes the Rubik’s Cube and prints it in the Planar Representation Format.
Random Shuffle: A function that returns a randomly shuffled Rubik’s Cube which is solvable.
isSolved(): a boolean function that tells whether the current configuration of the Rubik’s Cube is solved or not.

 

Some Key Concepts
 

Not all permutations are solvable

It is important to realize that taking 9 * 6 = 54 colors and randomly assigning them to some cube side will not create a solvable Rubik’s Cube. For eg: an Edge Cubie with both sides as Red, or a Corner Cubie with sides white-yellow-red. We can never solve such a Rubik’s Cube configuration. It turns out we can only reach one-twelfth of the total possible permutations from a solved Rubik’s Cube (https://qr.ae/pGztcM for more info).

Therefore, in the Random Shuffle function, it is important to generate a Rubik’s Cube that is solvable. For this we would use the pre-existing operations that are implemented, that is, F, Fprime, etc. We would take a solved Rubik’s Cube and take a random operation out of the 18 possible total operations and apply it to Rubik’s Cube and repeat this process some number of times. This way we will ensure that the configuration that we created is solvable by legal moves.


 

Breaking the print function into two parts

Another key idea is about the print function. Instead of leaving the entire print functionality completely to the Derived classes, we can implement a generic print function in the abstract class itself. We can use a helper function ‘getColor’, which given a face, a row number, and a column number, would return the color of that face. And we can make this helper function virtual and leave its implementation to the Derived Classes. This would significantly reduce our efforts in writing the print functionality for each representation.


 

Reference Link for Task 1: 
https://github.com/shubhampatil11/rubiks-cube-solver/blob/main/Model/RubiksCube.h
https://github.com/shubhampatil11/rubiks-cube-solver/blob/main/Model/RubiksCube.cpp