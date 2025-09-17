Rubik’s Cube Solver

A C++ Rubik’s Cube solver project implementing multiple cube representations, a variety of search algorithms, and a pattern-database (PDB) pipeline for heuristic search.

Tech stack: C++ (C++14), CMake
Status: Educational / experimental solver with PDB support (corner PDB included)

Table of contents

Features

Repository structure

Build instructions

Usage

Algorithms & Representations

Pattern database pipeline

Benchmarking guide

Developing / Testing

Notes & caveats

License

Contact

Features

Multiple cube state representations:

1D array representation

3D array representation

Bitboard representation

Search algorithms:

Breadth-First Search (BFS)

Depth-First Search (DFS)

Iterative Deepening DFS (IDDFS)

Iterative Deepening A* (IDA*) with corner PDB heuristic

Pattern database utilities:

Corner pattern database implementation

Permutation indexer helpers

Nibble-compressed storage for compact PDBs

CLI driver in main.cpp (interactive and/or demo modes—see usage)

Repository structure
.
├─ CMakeLists.txt
├─ main.cpp
├─ Model/
│  ├─ RubiksCube.cpp / .h
│  ├─ RubiksCube1dArray.cpp / .h
│  ├─ RubiksCube3dArray.cpp / .h
│  └─ RubiksCubeBitboard.cpp / .h
├─ Solver/
│  ├─ BFSSolver.h
│  ├─ DFSSolver.h
│  ├─ IDDFSSolver.h
│  └─ IDAstarSolver.h
├─ PatternDatabases/
│  ├─ PatternDatabase.cpp / .h
│  ├─ CornerPatternDatabase.cpp / .h
│  ├─ CornerDBMaker.cpp / .h
│  ├─ PermutationIndexer.h
│  ├─ NibbleArray.cpp / .h
│  └─ math.cpp / .h
└─ README.md
