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

## Refinement 5: Made Difference Reduction Explicit

### Summary
Added an explicit Knowledge relation showing that operators are selected because they reduce differences between the current state and the goal state.

### Changes

#### reducesDifference
- Added the `reducesDifference` relation from `operator` to `difference`.
- This captures the lesson's explanation that Means-Ends Analysis chooses operators that help reduce the difference between the current state and the goal state.

### Rationale
The previous model represented difference reduction procedurally through `SelectDifferenceReducingOperator` and the Method transition conditions, but the Knowledge model did not directly encode the relationship between operators and differences. Adding this relation makes the means-end link explicit: the operator is the means, and reducing the difference is the end.

## Refinement 6: Added Heuristic Concept

### Summary
Added an explicit `heuristic` concept to represent the rule of thumb used by Means-Ends Analysis to guide search from the initial state toward the goal state.

### Changes

#### heuristic
- Added the `heuristic` concept.
- Represents a rule of thumb for estimating which operator or state is most promising during search.
- Included because the lesson states that Means-Ends Analysis uses a heuristic to guide the search from the initial state to the goal state.

### Rationale
The previous Knowledge model described `WeakMethod` as heuristic-like, but it did not define `heuristic` itself. Adding this concept makes the lesson's search-guidance mechanism explicit and separates the general category of weak methods from the specific guidance principle used during Means-Ends Analysis.

## Refinement 7: Added Problem-Solving Method Concepts

### Summary
Expanded the Knowledge model with additional concepts from the lesson's discussion of problem reduction, universal methods, weak methods, and strong methods.

### Changes

#### ProblemReduction
- Added the `ProblemReduction` concept.
- Represents decomposing a difficult problem into smaller subproblems or subgoals.
- Included because the lesson uses problem reduction to help overcome obstacles encountered during Means-Ends Analysis.

#### Subgoal
- Added the `Subgoal` concept.
- Represents a smaller goal produced by decomposing a larger goal.
- Supports the lesson's explanation that problem reduction solves a larger problem by solving smaller pieces.

#### UniversalMethod
- Added the `UniversalMethod` concept.
- Represents a general-purpose problem-solving method applicable across a broad class of problems.
- Included because the lesson characterizes Means-Ends Analysis, Generate and Test, and Problem Reduction as universal methods.

#### StrongMethod
- Added the `StrongMethod` concept.
- Represents a knowledge-intensive problem-solving method that uses substantial domain knowledge to solve problems efficiently.
- Included to contrast with weak methods, which make little use of knowledge.

### Rationale
The prior Knowledge model represented `WeakMethod`, but it did not capture the broader method taxonomy from the lesson. Adding these concepts makes the model better reflect the lesson's distinction between universal weak methods and more knowledge-intensive strong methods, while also representing problem reduction and subgoals as important companions to Means-Ends Analysis.
