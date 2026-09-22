# Wheelchair-Friendly Campus Navigation using A*, an Accessibility-Aware Heuristic, and Dijkstra's Algorithm

## 1. Project Overview

This project implements a wheelchair-friendly navigation system for a simulated two-level campus environment.

The system models campus locations as nodes in a weighted graph and accessible pathways as edges. It uses shortest-path search algorithms to determine routes between locations while considering distance and accessibility-related constraints such as slope, rough surfaces, missing kerb ramps, obstacles, and level transitions.

The project implements and evaluates:

- A* Search with a Euclidean-distance heuristic
- A* Search with an accessibility-aware gateway heuristic
- Dijkstra's Algorithm as an uninformed shortest-path baseline
- An adjacency-matrix graph representation
- Accessibility-aware edge costs
- Connector closures
- Deterministic validation and experimental evaluation
- A Flask + React/Vite graphical user interface

The campus environment is **simulated and deterministic**. Accessibility values, distances, penalties, and constraints are model assumptions created for the purpose of evaluating the navigation algorithms. They are not measurements of a real campus.

---

## 2. Project Objectives

The project investigates how informed and uninformed search algorithms perform when navigating an accessibility-constrained environment.

The main objectives are to:

1. Construct a campus navigation environment containing accessible and constrained pathways.
2. Implement A* Search using an adjacency matrix.
3. Develop an accessibility-aware heuristic for a two-level environment.
4. Compare A* with Dijkstra's Algorithm.
5. Evaluate route selection under different accessibility-cost settings.
6. Investigate algorithm behaviour as graph size and constraint density increase.
7. Provide an interactive GUI for visualising and testing routes.

---

## 3. Environment

The final environment contains:

- **32 nodes**
- **51 path segments**
- **2 campus levels**
- **3 level-transition connectors**
- **48 ordinary segments**
- **3 connector segments**

The environment is represented using an adjacency matrix.

Each segment has attributes including:

- Length
- Slope
- Surface roughness
- Kerb-ramp availability
- Obstacle presence
- Level information
- Connector information where applicable

The environment is deterministic so that the experiments can be reproduced consistently.

---

## 4. Accessibility Cost Model

The routing system supports a configurable accessibility parameter `alpha`.

The cost of an edge is calculated as:

```text
cost = L × (1 + alpha × (slope / 5 + rough))
       + alpha × feature_penalty
       
