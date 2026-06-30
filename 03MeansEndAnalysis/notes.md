# TMK Refinement Notes

## Refinement 3: Added New Concepts

### Summary
Expanded the Knowledge model by adding concepts that were described in the lesson but were absent from the initial TMK model.

### Changes

#### WeakMethod
- Added the `WeakMethod` concept.
- Represents a heuristic or strategy that guides problem solving without guaranteeing an optimal or complete solution.
- Included because Means-Ends Analysis is characterized as a weak method in the lesson.

#### InitialState
- Added the `InitialState` concept.
- Represents the starting configuration of the problem before any operators are applied.
- Used to compare against the goal state when identifying differences.

#### GoalState
- Added the `GoalState` concept.
- Represents the desired target configuration that the problem solver aims to achieve.
- Used throughout Means-Ends Analysis to determine whether the problem has been solved.

### Rationale
The original TMK model focused on operators and configurations but omitted several core concepts introduced in the lesson. Adding these concepts improves instructional alignment by explicitly representing the fundamental elements of Means-Ends Analysis and better supports the iterative reasoning process described in the source material.