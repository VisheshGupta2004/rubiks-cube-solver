# Rubik's Cube Solver

[![C++](https://img.shields.io/badge/C++-14%2F17-blue.svg)](https://en.cppreference.com/)
[![CMake](https://img.shields.io/badge/CMake-3.20%2B-brightgreen)](https://cmake.org/)
[![License](https://img.shields.io/badge/License-MIT-orange.svg)](LICENSE)

A high-performance Rubik's Cube solver implemented in C++ featuring multiple solving algorithms and cube representations. This project demonstrates various search algorithms and pattern databases to efficiently solve the 3x3 Rubik's Cube.

## 🎯 Features

- **Multiple Cube Representations**:

  - 3D Array
  - 1D Array
  - Bitboard (for optimized performance)
- **Advanced Solving Algorithms**:

  - Breadth-First Search (BFS)
  - Depth-First Search (DFS)
  - Iterative Deepening DFS (IDDFS)
  - IDA* Search with Pattern Database Heuristics
- **Pattern Database Support**:

  - Corner Pattern Database for efficient solving
  - Optimized memory usage with Nibble Array storage

## 🚀 Getting Started

### Prerequisites

- C++14 or later
- CMake 3.20 or later
- Make or Ninja build system

### Building the Project

```bash
# Create build directory
mkdir -p build
cd build

# Configure with CMake
cmake ..

# Build the project
cmake --build .
```

### Running the Solver

```bash
# Run the solver
./rubiks_cube_solver
```

## 🧩 Project Structure

```
rubiks-cube-solver/
├── CMakeLists.txt       # CMake build configuration
├── Model/               # Core cube model implementations
│   ├── RubiksCube.h     # Base Rubik's Cube interface
│   ├── RubiksCube3dArray.cpp/.h  # 3D array implementation
│   ├── RubiksCube1dArray.cpp/.h  # 1D array implementation
│   └── RubiksCubeBitboard.cpp/.h # Bitboard implementation
├── Solver/              # Solving algorithms
│   ├── BFSSolver.h      # BFS implementation
│   ├── DFSSolver.h      # DFS implementation
│   ├── IDDFSSolver.h    # IDDFS implementation
│   └── IDAstarSolver.h  # IDA* with pattern database
├── PatternDatabases/    # Pattern database implementations
│   ├── CornerDBMaker.cpp/.h
│   ├── CornerPatternDatabase.cpp/.h
│   └── NibbleArray.cpp/.h
└── main.cpp             # Main entry point
```

## 🧠 Algorithms

### 1. Breadth-First Search (BFS)

- **Type**: Uninformed Search
- **Description**: Explores all possible moves level by level, guaranteeing an optimal solution (shortest path).
- **Best For**: Finding the shortest solution path
- **Time Complexity**: O(b^d), where b is branching factor and d is depth of solution
- **Space Complexity**: O(b^d)
- **Limitations**: High memory usage due to exponential growth of nodes

### 2. Depth-First Search (DFS)

- **Type**: Uninformed Search
- **Description**: Explores as far as possible along each branch before backtracking.
- **Best For**: Memory efficiency in deep trees
- **Time Complexity**: O(b^m), where m is the maximum depth
- **Space Complexity**: O(b*m)
- **Limitations**: Not guaranteed to find the shortest path, can get stuck in deep paths

### 3. Iterative Deepening DFS (IDDFS)

- **Type**: Uninformed Search
- **Description**: Combines benefits of BFS and DFS by performing DFS with increasing depth limits.
- **Best For**: When the solution depth is unknown but optimality is required
- **Time Complexity**: O(b^d), same as BFS but with better space complexity
- **Space Complexity**: O(b*d)
- **Advantages**:
  - Finds the shortest path like BFS
  - Uses less memory than BFS
  - Handles infinite paths better than DFS

### 4. IDA* with Pattern Databases

- **Type**: Informed Search (Heuristic-based)
- **Description**: Combines IDDFS with a heuristic function to guide the search more efficiently.
- **Time Complexity**: O(b^d)
- **Space Complexity**: O(d)
- **Key Components**:
  - Uses a corner pattern database as an admissible heuristic
  - Precomputes minimum moves required to solve corner cubies
  - Significantly reduces the search space
- **Performance**:
  - Memory efficient (uses nibble arrays for pattern databases)
  - Fast solving with optimized pruning
  - Flexible across different cube representations

### Performance Comparison

| Algorithm | Optimal Solution | Time Complexity | Space Complexity | Best Use Case |
| --------- | ---------------- | --------------- | ---------------- | ------------- |
| BFS       | Yes              | O(b^d)          | O(b^d)           | Shortest path |
| DFS       | No               | O(b^m)          | O(b*m)           | Memory saving |
| IDDFS     | Yes              | O(b^d)          | O(b*d)           | Unknown depth |
| IDA*      | Yes              | O(b^d)          | O(d)             | Large puzzles |

## 📚 Documentation

### Cube Notation

The solver uses standard cube notation:

- **F, B, U, D, L, R**: Clockwise face turns
- **F', B', U', D', L', R'**: Counter-clockwise face turns
- **F2, B2, U2, D2, L2, R2**: 180-degree face turns

To implement additional solving methods or cube representations, extend the base `RubiksCube` class and implement the required interface methods.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style

- Follow Google C++ Style Guide
- Use meaningful variable and function names
- Add comments for complex logic
- Keep lines under 100 characters
- Use 4 spaces for indentation

## 🙏 Acknowledgments

- Inspired by various Rubik's Cube solving algorithms and optimizations
- Special thanks to the open-source community for their contributions to algorithm education
