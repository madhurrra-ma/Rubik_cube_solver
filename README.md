# 🧩 Rubik's Cube Solver

I explored this Rubik's Cube Solver project to better understand how classical search algorithms can be applied to solve real-world state-space problems.

While working through the code, I spent time understanding how different cube representations affect performance and how informed search algorithms can significantly reduce the number of explored states.

The project is written in C++ and includes multiple solving approaches along with different ways of representing the cube internally.

---

## About the Project

I worked on this project to explore how search algorithms and heuristic techniques can be applied to solve complex combinatorial problems like the Rubik's Cube.

While building and studying this project, I gained hands-on experience with:

- Object-Oriented Programming in C++
- State space search
- Graph traversal algorithms
- Heuristic search techniques
- Pattern Databases
- Bit manipulation for efficient state representation

This project strengthened my understanding of algorithm optimization and software design while working with a real-world problem.

---

## Features

- Supports multiple Rubik's Cube representations
- Implements several search algorithms
- Uses Pattern Database heuristics for faster solving
- Modular and object-oriented code structure
- Optimized state representation using bit manipulation
- Easily extensible architecture for adding new solving algorithms

---

## Technologies Used

- C++
- Standard Template Library (STL)
- Object-Oriented Programming
- Graph Algorithms
- Heuristic Search
- Bit Manipulation

---

## 🧠 Algorithms Implemented

### Depth First Search (DFS)

Explores one branch completely before backtracking. It requires less memory but does not always produce the shortest solution.

---

### Breadth First Search (BFS)

Searches level by level and guarantees the shortest solution, although it consumes significant memory.

---

### Iterative Deepening DFS (IDDFS)

Combines the low memory usage of DFS with the optimality of BFS by increasing the search depth iteratively.

---

### Iterative Deepening A* (IDA*)

Uses heuristic estimates from Pattern Databases to efficiently search the solution space while minimizing memory consumption.

---



## Concepts Explored

- State Space Representation
- Graph Traversal
- Search Algorithms
- Heuristic Functions
- Pattern Databases
- Memory Optimization
- Bit Manipulation
- Object-Oriented Design

---

## Challenges

Some interesting challenges while working on this project included:

- Representing cube states efficiently
- Reducing search complexity
- Optimizing memory usage
- Understanding heuristic-based search
- Organizing modular C++ code

---

## Future Improvements

- Interactive command-line interface
- Random scramble generator
- Performance comparison between algorithms
- Solution visualization
- Move history playback
- Graphical user interface (GUI)

---

## What I Learned

Working with this project helped me understand:

How a Rubik's Cube can be represented in different data structures
The difference between uninformed and heuristic search algorithms
Why IDA* performs much better than DFS or BFS for large search spaces
How Pattern Databases improve search efficiency
Organizing a larger C++ project into reusable modules

Acknowledgement

This project is intended for educational and learning purposes.
