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

## Refinement 4: Corrected Method Completion Logic

### Summary
Refined the Method model so that Means-Ends Analysis continues iterating until the goal state is reached, rather than treating any reduction in difference as a complete solution.

### Changes

#### Current State Tracking
- Added method initialization: `currentState = initialConfiguration`.
- Updated the comparison step to compare `currentState` against `goalConfiguration`.
- This allows the method to reason over the evolving state after each operator is applied.

#### Completion Condition
- Replaced the `S3 -> S4_Complete` transition condition from `reducesDifference(newState)` to `goodSolution(newState)`.
- This aligns completion with the Knowledge assertion that a good solution has zero difference between the current state and the goal state.

#### Iterative Loop
- Added a loop from `S3` back to `S0` when `reducesDifference(newState) && !goodSolution(newState)`.
- Added the data effect `currentState = newState` so the next comparison uses the updated state.

### Rationale
The lesson describes Means-Ends Analysis as a repeated cycle: compare the current state to the goal state, select an operator that reduces the difference, apply it, and continue until the goal is reached. A state that reduces the difference is progress, not necessarily success. This refinement keeps the existing `GoalState`, `finalConfiguration`, and `goodSolution` knowledge elements intact while making the Method model use them correctly.
