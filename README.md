# Rubik’s Cube Solver

An educational/experimental Rubik’s Cube solver in **C++ (C++14)** with multiple cube representations, several search algorithms, and a pattern-database (PDB) pipeline for heuristic search. Includes a corner PDB implementation.

---


## Features

* Multiple cube state representations:

  * 1D array representation
  * 3D array representation
  * Bitboard representation

* Search algorithms:

  * Breadth-First Search (BFS)
  * Depth-First Search (DFS)
  * Iterative Deepening DFS (IDDFS)
  * Iterative Deepening A\* (IDA\*) using the corner PDB heuristic

* Pattern database utilities:

  * Corner pattern database implementation
  * Permutation indexer helpers
  * Nibble-compressed storage for compact PDBs

* CLI driver in `main.cpp` (interactive and/or demo modes — see Usage)

---

## Repository structure

```
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
├─ scripts/ (optional)
│  └─ run_bench.sh
├─ BENCHMARK.md (recommended)
└─ README.md
```



## Algorithms & Representations

### Representations

* **1D array**: compact and easy for direct indexing.
* **3D array**: intuitive mapping to faces.
* **Bitboard**: memory-compact and often faster using bitwise ops.

You can switch implementations by constructing a different `RubiksCube` derived class or adjusting the driver.

### Solvers

* **BFS**: complete; useful for very small depths.
* **DFS / IDDFS**: simple deep search; IDDFS uses iterative limits.
* **IDA\***: iterative deepening A\* with `f = g + h` using PDB heuristics. With stronger PDBs it can find optimal or near-optimal solutions.

---

## Pattern database pipeline

* Utilities to **generate** corner pattern databases (`CornerDBMaker`) and store them in a nibble-packed format to reduce disk usage.
* **Permutation indexer** helpers to map permutations ↔ indices for fast PDB lookups.
* Load PDB files at startup to be used as heuristics for IDA\*.
* Note: only the **corner PDB** is included by default. Adding edge PDBs increases heuristic strength (Korf’s approach uses corner + two edge PDBs).

---

## Benchmarking guide

Add/enable a benchmark mode (if not present): create a harness that:

   * Generates `N` random scrambles of fixed length `L` (e.g., 8 or 13).
   * Runs the chosen solver on each scramble.
   * Measures and records:

     * wall time (ms) per solve
     * solution length (moves)
     * nodes expanded / pruned (add counters in solver)
     * PDB load time and size (if using PDBs)

Example run (adapt flags to your CLI):

   ```bash
   ./rubiks_cube_solver --benchmark --solver ida --rep bitboard --scramble-length 13 --trials 50
   ```


* Use `std::chrono::high_resolution_clock` for timing.
* Run experiments multiple times and report median/95th percentile.
* Add counters in hot paths (nodes expanded, prunes, peak frontier).




### Small examples / snippets (optional)

**Example: run IDA* with bitboard representation (CLI example — adapt to your `main.cpp` flags)*\*

```bash
./rubiks_cube_solver --solver ida --rep bitboard "R U R' U' F2"
```
