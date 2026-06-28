Bitboard Representation (6 64-bit Integers)
After the array representations of Rubik’s Cube, let’s come to something more faster and compact, that is, bits. Let’s see how we can use bits to represent the Rubik’s Cube.

There are 6 unique colors in a Rubik’s Cube. For every color, let’s try to represent it in an 8-bit format. Out of the 8-bits, only one bit would be set (1), and its position would define the color. For example, we encode the colors as follows: 

 

Color	8-bit Format
White 	00000001
Green 	00000010
Red 	00000100
Blue 	00001000
Orange 	00010000
Yellow 	00100000
 

White has its 0th-bit set. Green has its 1st-bit set. And so on. The last two bits would always be 0 because there are only 6 colors.

Note that we are keeping the order of the colors and faces uniform in all the representations. This makes it simple to implement and remember things. 

 

The order we use is

Color	White	Green	Red	Blue	Orange	Yellow
Face	Up	Left	Front	Right	Back	Down
 

We are done with representing a color. Let’s try to represent a face. 

 

A face has 9 colors/stickers. Since the center stickers are always stationary, we only need to store 8 out of the 9 stickers. We can use the 8-bit format for each sticker.

8 (stickers) * 8 (8-bit color) = 64 bits. 

 

Therefore, each face can be represented using a 64-bit integer.

The first 8 bits of the integer would represent the 0th index sticker. The next 8 bits would represent the 1st index sticker. And so on.

 

We index the stickers in a face in a clockwise rotational fashion, like below:

0    1    2

7    _    3

6    5    4

 

So finally an example face would look something like this: 

64-bit format: 

Color	G	W	Y	O	B	R	G	W
Bits	00000010 	00000001 	00100000 	00010000 	00001000 	00000100 	00000010	00000001 
Index	7	6	5	4	3	2	1	0
 

The 64-bit integer would be:

00000010 00000001 00100000 00010000 00001000 00000100 00000010 00000001

In the Decimal, the above representation is equivalent to the number 144431916278612481.

 

This face would look something like this:

W    G    R

G     _     B

W    Y    O


 

We can create an array of 6 64-bit integers, bitboard[6],  to represent the whole cube.


bitboard[ i ] → the 64-bit integer representing the ith face.


Task 4: Bitboard Representation
Write an implementation of the bitboard representation of the Rubik’s Cube as described above. Derive this class from the generic Rubik’s Cube we designed in Task 1. Implement all the necessary functions (all the virtual functions).


Some Key Concepts
Keeping indices of the cube in a clockwise rotational fashion

This idea helps us greatly in rotating a particular face. While doing any operation this idea makes it very easy to do a face rotation. We just need to rotate the 64-bit integer by 16 bits and the face would be rotated. Next, we can adjust the adjacent sides of the face manually.


For example if want to rotate the front face and it looks something like this:

W    G    R

G     _     B

W    Y    O


Which sequentially translates to : 

Color:    W     G     R     B     O     Y     W     G

Index:    0      1      2     3     4      5      6      7


After rotation the face would look something like:

W     G     W

Y      _      G

O      B     R


Which sequentially translates to:


Color: W G W G R B O Y

Index: 0 1 2 3 4 5 6 7


If you look carefully, we have just shifted the number by two indices (8 bits * 2 = 16 bits), and put the last two indices in the first.


Caution: Don’t get confused by seeing indices written here in increasing order from left-to-right. In actual, bit form they will be opposite, as the 0th index would occupy bits from 0 to 7, 1st index from 8 to 15, and so on.


This makes it very easy to rotate the face. But we still need to adjust the rest of the faces that got affected due to rotation. 

In case of a F move, some of the top cubbies will come to right, some right cubbies to down, down to left, and some left cubbies to top. We need to adjust those manually in code.

 

 
Reference Link for Task 4: 
https://github.com/shubhampatil11/rubiks-cube-solver/blob/main/Model/RubiksCubeBitboard.cpp