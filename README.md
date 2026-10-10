# warehouse-delivery-robot
# Warehouse Delivery Robot: Search Algorithms

Intelligent Systems, Task 1, Alexandria University.

A robot in a warehouse must move from the start cell `S` to the goal cell `G` on a grid map. It moves Up, Down, Left or Right (one cell at a time) and cannot enter a wall. This project finds the path using search algorithms implemented from scratch (no path-finding libraries).

| Symbol | Meaning |
|---|---|
| `S` / `G` | Start cell / Goal cell (entering G costs 1, S is not counted) |
| `.` | Normal floor (cost 1) |
| `~` | Rough floor (cost 3) |
| `#` | Wall (cannot enter) |

## Algorithms

- **UCS (Uniform Cost Search)**: uninformed. Expands the node with the lowest cost so far, g(n).
- **A\***: informed. Expands the node with the lowest f(n) = g(n) + h(n), with Manhattan distance as the heuristic.
- **BFS** (extra): fewest steps, ignores costs. Included only to show the trap in MAP_B.

For each run the program prints the algorithm name, the path as a list of `(row, column)`, the path cost, the number of nodes expanded, and the map with the path marked by `*`. If there is no path it prints `No path found`. A summary table (path length, cost, nodes expanded, max frontier size, run time) is printed at the end.

## Requirements

- Python 3.8 or newer
- No external libraries (only `heapq`, `collections`, `time`, `sys` from the standard library)

## How to run

Run every algorithm on MAP_A, MAP_B and MAP_C:

```bash
python warehouse_robot.py
```

Run on a single map:

```bash
python warehouse_robot.py --only
```

## How to change the map

Open `warehouse_robot.py` and edit this line near the top:

```python
GRID = MAP_A   # change to MAP_B, MAP_C, or your own map
```

Then run with `--only`. You can also define your own map as a list of strings, one string per row:

```python
MY_MAP = [
    "S..#",
    ".#..",
    "...G",
]
GRID = MY_MAP
```

`S` and `G` are found automatically by scanning the grid.

## Results

Path length is the number of moves. Run times vary slightly between machines.

| Map | Algorithm | Path length | Path cost | Nodes expanded | Max frontier |
|---|---|---|---|---|---|
| MAP_A | UCS | 11 | 15 | 28 | 4 |
| MAP_A | A* | 11 | 15 | 21 | 5 |
| MAP_B | UCS | 12 | 12 | 30 | 4 |
| MAP_B | A* | 12 | 12 | 15 | 7 |
| MAP_B | BFS (extra) | 8 | 22 | 25 | 4 |
| MAP_C | UCS | No path found | - | 13 | 3 |
| MAP_C | A* | No path found | - | 13 | 3 |

## Key findings

- UCS and A* both find the optimal path (cost 15 on MAP_A, cost 12 on MAP_B).
- A* expands fewer nodes than UCS (21 vs 28 on MAP_A, 15 vs 30 on MAP_B) because the heuristic guides the search toward the goal.
- On MAP_B, BFS finds the shortest path in steps (8 moves) but it costs 22, almost double the optimal cost of 12, because it crosses rough floor.
- MAP_C has no solution, and both algorithms correctly report `No path found`.
- For this robot, A* with Manhattan distance is the best choice: optimal, and faster than UCS.

## Team

- Youssef Ahmed Hamedo (2403242213)
- Youssef Sherif Ahmed (2403244508)
- Mostafa Khamis (2403242142)
