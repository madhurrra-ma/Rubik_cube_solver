# Rubik's Cube Solver - Comprehensive Tutorial

## Table of Contents
1. [Object-Oriented Programming (OOP) Fundamentals](#oop-fundamentals)
2. [Project Overview](#project-overview)
3. [Architecture & Design](#architecture--design)
4. [Code Explanation](#code-explanation)
5. [Getting Started](#getting-started)
6. [Usage Examples](#usage-examples)
7. [Algorithm Comparison](#algorithm-comparison)

---

## OOP Fundamentals

Before diving into the code, let's understand key OOP concepts used in this project:

### 1. **Classes & Objects**
A **class** is a blueprint for creating objects. An **object** is an instance of a class.

```cpp
// Example:
RubiksCubeBitboard cube;  // 'cube' is an object of class RubiksCubeBitboard
```

### 2. **Encapsulation**
Bundling data (attributes) and methods (functions) together. Data hiding protects internal state.

```cpp
class RubiksCube {
private:
    // Hidden internal representation
    int state;
    
public:
    // Public interface
    void u();  // Up face rotation
    bool isSolved();
};
```

### 3. **Inheritance**
Multiple cube representations (3D Array, 1D Array, Bitboard) inherit from a base `RubiksCube` class, sharing common interface.

```cpp
class RubiksCube3dArray : public RubiksCube { };
class RubiksCube1dArray : public RubiksCube { };
class RubiksCubeBitboard : public RubiksCube { };
```

### 4. **Polymorphism**
Different cube types implement the same methods differently:

```cpp
// All cube types support these operations:
cube.u();      // Rotate up face
cube.l();      // Rotate left face
cube.print();  // Display state
```

### 5. **Templates (Generics)**
Write solver code once, use with any cube type:

```cpp
template<typename CubeType, typename HashType>
class DFSSolver {
    // Works with RubiksCube3dArray, RubiksCube1dArray, RubiksCubeBitboard
};
```

---

## Project Overview

This is a **Rubik's Cube Solver** that finds optimal solutions using multiple search algorithms.

### Key Components:

| Component | Purpose |
|-----------|---------|
| **Model** | Represents cube state (3 different implementations) |
| **Solver** | Finds solution using various algorithms |
| **PatternDatabase** | Heuristic for faster solving |

---

## Architecture & Design

### 1. **Cube Representations** (3 Models)

#### **RubiksCube3dArray**
- Stores cube state in a 3D array
- Intuitive but memory-heavy
- Good for learning

#### **RubiksCube1dArray**
- Flattens 3D into 1D array
- More memory efficient

#### **RubiksCubeBitboard**
- Uses bitwise operations
- Most efficient, fastest
- Compact state representation

### 2. **Solvers** (4 Algorithms)

#### **DFS (Depth-First Search)**
- Simple exhaustive search
- May require large depth limits
- Good for small depths

#### **BFS (Breadth-First Search)**
- Explores layer by layer
- Guarantees shortest path
- Memory intensive for large spaces

#### **IDDFS (Iterative Deepening DFS)**
- Combines DFS efficiency with BFS optimality
- Better memory usage than BFS

#### **IDA* (Iterative Deepening A*)**
- Best performance
- Uses heuristics (Pattern Database)
- Finds solutions efficiently

### 3. **Pattern Database**
- Pre-computed lookup table
- Stores minimum moves for corner positions
- Heuristic guidance for IDA* solver

---

## Code Explanation

### **main.cpp Overview**

```cpp
#include <bits/stdc++.h>
```
Includes all standard C++ libraries (convenience header).

### **Cube Representations (Available Models)**

```cpp
//#include "Model/RubiksCube3dArray.cpp"
//#include "Model/RubiksCube1dArray.cpp"
//#include "Model/RubiksCubeBitboard.cpp"
```

Each representation implements the same interface with different storage strategies.

### **Solvers Available**

```cpp
#include "Solver/DFSSolver.h"
#include "Solver/BFSSolver.h"
#include "Solver/IDDFSSolver.h"
#include "Solver/IDAstarSolver.h"
```

Different solving algorithms to choose from.

### **Main Function - Code Sections**

#### **Section 1: Testing Models (Commented)**
```cpp
RubiksCube3dArray object3DArray;
if (object3DArray.isSolved()) cout << "SOLVED\n";
object3DArray.u();  // Rotate up face
object3DArray.print();  // Display state
```

**What happens:**
1. Create a solved cube
2. Check if solved (should be true)
3. Apply move (U - up rotation)
4. Check if solved (should be false)
5. Print the cube state

#### **Section 2: DFS Solver (Commented)**
```cpp
RubiksCube3dArray cube;
cube.print();

vector<RubiksCube::MOVE> shuffle_moves = cube.randomShuffleCube(6);
for (auto move: shuffle_moves) cout << cube.getMove(move) << " ";
cout << "\n";
cube.print();

DFSSolver<RubiksCube3dArray, Hash3d> dfsSolver(cube, 8);
vector<RubiksCube::MOVE> solve_moves = dfsSolver.solve();
```

**What happens:**
1. Create a solved cube
2. Randomly shuffle it (6 moves)
3. Print shuffle moves
4. Create DFS solver (max depth 8)
5. Solve and get solution moves
6. Print solution

#### **Section 3: BFS Solver (Commented)**
```cpp
RubiksCubeBitboard cube;
cube.print();

vector<RubiksCube::MOVE> shuffle_moves = cube.randomShuffleCube(6);
for(auto move: shuffle_moves) cout << cube.getMove(move) << " ";

BFSSolver<RubiksCubeBitboard, HashBitboard> bfsSolver(cube);
vector<RubiksCube::MOVE> solve_moves = bfsSolver.solve();
```

**What happens:**
1. Create bitboard cube (efficient)
2. Shuffle with 6 moves
3. Create BFS solver
4. Find optimal solution
5. Print solution path

#### **Section 4: IDDFS Solver (Commented)**
```cpp
RubiksCubeBitboard cube;
vector<RubiksCube::MOVE> shuffle_moves = cube.randomShuffleCube(7);

IDDFSSolver<RubiksCubeBitboard, HashBitboard> iddfsSolver(cube, 7);
vector<RubiksCube::MOVE> solve_moves = iddfsSolver.solve();
```

**What happens:**
1. Shuffle with 7 moves
2. Create IDDFS solver
3. Iteratively deepen search
4. Find solution efficiently

#### **Section 5: IDA* Solver (Commented)**
```cpp
RubiksCubeBitboard cube;
vector<RubiksCube::MOVE> shuffle_moves = cube.randomShuffleCube(5);

IDAstarSolver<RubiksCubeBitboard, HashBitboard> idAstarSolver(cube);
vector<RubiksCube::MOVE> solve_moves = idAstarSolver.solve();
```

**What happens:**
1. Shuffle with 5 moves
2. Create IDA* solver
3. Use heuristic guidance
4. Find solution quickly

#### **Section 6: Pattern Database & IDA* (ACTIVE CODE)**

```cpp
string fileName = "C:\\Users\\user\\CLionProjects\\rubiks-cube-solver\\Databases\\cornerDepth5V1.txt";

RubiksCubeBitboard cube;
auto shuffleMoves = cube.randomShuffleCube(13);
cube.print();
for (auto move: shuffleMoves) cout << cube.getMove(move) << " ";
cout << "\n";

IDAstarSolver<RubiksCubeBitboard, HashBitboard> idaStarSolver(cube, fileName);
auto moves = idaStarSolver.solve();

idaStarSolver.rubiksCube.print();
for (auto move: moves) cout << cube.getMove(move) << " ";
cout << "\n";
```

**What happens:**
1. Load pattern database from file
2. Create a bitboard cube (most efficient)
3. Shuffle it with 13 random moves
4. Print initial scrambled state
5. Print all shuffle moves
6. Create IDA* solver with database heuristic
7. Solve using intelligent search
8. Print final solved state
9. Print solution moves

---

## Getting Started

### Prerequisites
- C++ compiler (C++11 or later)
- Pattern database file (optional, for IDA* enhancement)

### Compilation

```bash
cd /Users/ayushchoudhary/Rubiks\ Cube\ Solver/rubiks-cube-solver/
g++ -std=c++17 main.cpp -o solver
```

### Running

```bash
./solver
```

---

## Usage Examples

### **1. Basic Cube Operations**

```cpp
RubiksCubeBitboard cube;  // Create solved cube
cube.u();     // Rotate UP face clockwise
cube.uPrime(); // Rotate UP face counter-clockwise
cube.l();     // Rotate LEFT face
cube.lPrime(); // Rotate LEFT face counter-clockwise
cube.f();     // Rotate FRONT face
cube.fPrime(); // Rotate FRONT face counter-clockwise
cube.r();     // Rotate RIGHT face
cube.rPrime(); // Rotate RIGHT face counter-clockwise
cube.b();     // Rotate BACK face
cube.bPrime(); // Rotate BACK face counter-clockwise
cube.d();     // Rotate DOWN face
cube.dPrime(); // Rotate DOWN face counter-clockwise

cube.print(); // Display cube state
```

### **2. Shuffling & Checking**

```cpp
RubiksCubeBitboard cube;
vector<RubiksCube::MOVE> moves = cube.randomShuffleCube(10);  // 10 random moves

cout << "Shuffled with: ";
for (auto move: moves) cout << cube.getMove(move) << " ";
cout << "\n";

if (cube.isSolved()) cout << "Solved!";
else cout << "Not solved";
```

### **3. DFS Solving (Simple, Limited Depth)**

```cpp
RubiksCube3dArray cube;
cube.randomShuffleCube(5);

DFSSolver<RubiksCube3dArray, Hash3d> solver(cube, 10);  // Max depth 10
auto solution = solver.solve();

cout << "Solution: ";
for (auto move: solution) cout << cube.getMove(move) << " ";
```

### **4. BFS Solving (Optimal Path, Memory Heavy)**

```cpp
RubiksCubeBitboard cube;
cube.randomShuffleCube(6);

BFSSolver<RubiksCubeBitboard, HashBitboard> solver(cube);
auto solution = solver.solve();

cout << "Optimal solution (" << solution.size() << " moves): ";
for (auto move: solution) cout << cube.getMove(move) << " ";
```

### **5. IDDFS Solving (Balanced Approach)**

```cpp
RubiksCubeBitboard cube;
cube.randomShuffleCube(8);

IDDFSSolver<RubiksCubeBitboard, HashBitboard> solver(cube, 15);
auto solution = solver.solve();

cout << "Solution: ";
for (auto move: solution) cout << cube.getMove(move) << " ";
```

### **6. IDA* Solving (BEST - Fast & Optimal)**

```cpp
RubiksCubeBitboard cube;
cube.randomShuffleCube(13);

string dbPath = "path/to/cornerDepth5V1.txt";
IDAstarSolver<RubiksCubeBitboard, HashBitboard> solver(cube, dbPath);
auto solution = solver.solve();

cout << "Optimal solution: ";
for (auto move: solution) cout << cube.getMove(move) << " ";
```

### **7. Equality & Assignment**

```cpp
RubiksCubeBitboard cube1, cube2;
if (cube1 == cube2) cout << "Cubes are equal\n";

cube1.randomShuffleCube(1);
cube2 = cube1;  // Copy assignment
if (cube1 == cube2) cout << "Now they're equal\n";
```

### **8. Using Unordered Map (State Storage)**

```cpp
unordered_map<RubiksCubeBitboard, bool, HashBitboard> visited;

RubiksCubeBitboard cube;
visited[cube] = true;

if (visited[cube]) cout << "Cube state already seen\n";
```

---

## Algorithm Comparison

| Algorithm | Speed | Memory | Optimality | Best For |
|-----------|-------|--------|-----------|----------|
| DFS | Medium | Low | ✗ | Small depths |
| BFS | Medium | High | ✓ | Small problems |
| IDDFS | Medium | Low | ✓ | Medium problems |
| IDA* | **Fast** | **Low** | ✓ | **Large problems** |

---

## Key Takeaways

1. **Multiple Representations** - Same logic, different implementations (3D Array, 1D Array, Bitboard)
2. **Template Design** - Generic solvers work with any cube type
3. **Algorithm Choice** - Pick solver based on problem size and constraints
4. **Heuristics Matter** - Pattern databases make IDA* efficient
5. **OOP Power** - Inheritance & polymorphism enable clean, extensible code

---

## Tips for Development

- Start with simpler solvers (DFS/BFS) for understanding
- Use Bitboard representation for production (fastest)
- Build Pattern Databases for harder problems
- Test with small shuffle depths first (5-6 moves)
- Uncomment code sections in main.cpp to test different algorithms

---