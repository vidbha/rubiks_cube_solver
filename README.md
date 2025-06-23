# Rubik’s Cube Solver

Rubik’s Cube Solver is a C++ project for automatically solving the standard 3×3 Rubik’s Cube (a classic 3D combination puzzle invented in 1974). The 3×3 cube has about 4.3×10^19 (≈43 quintillion) possible configurations, so brute-force solving is infeasible. This project implements several search algorithms and heuristics to find solutions efficiently. It is written in C++ (using C++14 and CMake) and includes multiple cube representations (3D array, 1D array, and bitboard) to demonstrate performance differences.

## Features

### Algorithms Supported
- **Breadth-First Search (BFS)**: Explores moves level by level and is guaranteed to find the shortest solution if one exists. Requires significant memory.
- **Depth-First Search (DFS)**: Explores one branch deeply; uses very little memory but not guaranteed to find the shortest solution.
- **Iterative Deepening DFS (IDDFS)**: Combines DFS’s low memory with BFS’s completeness.
- **Iterative Deepening A\* (IDA\*)**: Extension of IDDFS using heuristics to prune the search. Uses a pattern-database heuristic for the cube.

### Pattern Database Heuristics
A pattern database (PDB) is a precomputed table of optimal distances for subsets of cube pieces. This solver includes a PDB for corner pieces, used as an admissible heuristic during IDA* search. The provided database (`cornerDepth5V1.txt`) was built using BFS from the solved state.

### Cube Representations
- `RubiksCube3dArray` – classic 3D matrix model.
- `RubiksCube1dArray` – linearized version.
- `RubiksCubeBitboard` – compact and efficient bitboard encoding.

## Build & Run (Cross-Platform)

Requires C++14 compiler and CMake (≥3.20). No external libraries needed.

```bash
# In the project root directory
mkdir build
cd build
cmake ..
make -j$(nproc)
```

This builds the `rubiks_cube_solver` executable in the `build/` directory.

Make sure `Databases/cornerDepth5V1.txt` is present. This file is the precomputed PDB used by the IDA* solver.

## Usage

```bash
./rubiks_cube_solver WWWWWWWWWGGGRRRBBBYYYOOOGGGRRRBBBYYYOOOGGGRRRBBBYYYOOO
```

Generates a random scramble (13 moves), displays the cube state, and solves it using IDA* (default). Example output:

```
Scramble moves: F U' R2 D L...
Solution moves: L2 U F' D' R...
```

You can modify `main.cpp` to use different solvers (e.g., BFS, IDDFS) or input your own scramble.

## Screenshot

**Example**: A Rubik’s Cube before and after solving. The solver prints the cube configuration and solution in text.

## Contribution

Contributions and feedback are welcome!

- **Issues**: Open one describing the problem or suggestion.
- **Pull Requests**: Fork and submit PRs. Minimal coding style.
- **Ideas**: Suggest solvers, GUI visualizations, or improved PDBs.

This is an educational showcase of Rubik’s Cube solving via search algorithms. Extend it with larger heuristics, performance benchmarks, or visualization tools.

